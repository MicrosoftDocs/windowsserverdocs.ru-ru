---
title: Сценарии вычислений для сети узла (ХКН)
ms.author: jmesser
author: jmesser81
ms.date: 11/05/2018
ms.openlocfilehash: c6b09ec65bd76fb63c2bb5c4eb5da1187f62ca75
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955681"
---
# <a name="common-scenarios"></a>Распространенные сценарии

>Область применения: Windows Server (половина ежегодного канала), Windows Server 2019

## <a name="scenario-hcn"></a>Сценарий: ХКН


### <a name="create-an-hcn"></a>Создание ХКН

В этом примере показано, как использовать API-интерфейс среды выполнения вычислений узла для создания сети вычислений узла на узле, который можно использовать для подключения виртуальных сетевых адаптеров к виртуальным машинам или контейнерам.

```C++
using unique_hcn_network = wil::unique_any<
    HCN_NETWORK,
    decltype(&HcnCloseNetwork),
    HcnCloseNetwork>;


/// Creates a simple HCN Network, waiting synchronously to finish the task
void CreateHcnNetwork()
{

    unique_hcn_network hcnnetwork;
    wil::unique_cotaskmem_string result;
    std::wstring settings = LR"(
    {
        "SchemaVersion": {
            "Major": 2,
            "Minor": 0
        },
        "Owner" : "WDAGNetwork",
        "Flags" : 0,
        "Type"  : 0,
        "Ipams" : [
            {
                "Type" : 0,
                "Subnets" : [
                    {
                        "IpAddressPrefix" : "192.168.1.0/24",
                        "Policies" : [
                            {
                                "Type" : "VLAN",
                                "IsolationId" : 100,
                            }
                        ],
                        "Routes" : [
                            {
                                "NextHop" : "192.168.1.1",
                                "DestinationPrefix" : "0.0.0.0/0",
                            }
                        ]

                    }
                ],
            },
        ],
        "MacPool":  {
            "Ranges" : [
                {
                    "EndMacAddress":  "00-15-5D-52-CF-FF",
                    "StartMacAddress":  "00-15-5D-52-C0-00"
                }
            ],
        },
        "Dns" : {
            "Suffix" : "net.home",
            "ServerList" : ["10.0.0.10"],
        }
    }
    })";

    GUID networkGuid;
    HRESULT result = CoCreateGuid(&networkGuid);

    result = HcnCreateNetwork(
        networkGuid,              // Unique ID
        settings.c_str(),      // Compute system settings document
        &hcnnetwork,
        &result
        );
    if (FAILED(result))
    {
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //    "ErrorCode" : <uint32>,
        //    "Error" : <string>,
        //    "Success" : <bool>,
       //   }

        // Failed to create network
        THROW_HR(result);
    }

    // Close the Handle
    result = HcnCloseNetwork(hcnnetwork.get());

    if (FAILED(result))
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }

}
```

### <a name="delete-an-hcn"></a>Удаление ХКН

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла, чтобы открыть & удалить расчетную сеть узла.

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID networkGuid; // Initialize it to appropriate network guid value
    HRESULT hr = HcnDeleteNetwork(networkGuid, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
```


### <a name="enumerate-all-networks"></a>Перечисление всех сетей

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для перечисления всех вычислений в составе узла.

```C++
     wil::unique_cotaskmem_string resultNetworks;
     wil::unique_cotaskmem_string errorRecord;

     // Filter to select Networks based on properties
     std::wstring filter [] = LR"(
     {
         "Name"  : "WDAG",
     })";
     HRESULT result = HcnEnumerateNetworks(filter.c_str(), &resultNetworks, &errorRecord);
     if (FAILED(result))
     {
         // UnMarshal  the result Json

         THROW_HR(result);
     }
```


### <a name="query-network-properties"></a>Запрос свойств сети

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для запроса свойств сети.

```C++
    unique_hcn_network hcnnetwork;
    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    {
        // Future
    })";
    GUID networkGuid; // Initialize it to appropriate network guid value
    HRESULT hr = HcnOpenNetwork(networkGuid, &hcnnetwork, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    hr = HcnQueryNetworkProperties(hcnnetwork.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


## <a name="scenario-hcn-endpoint"></a>Сценарий: конечная точка ХКН

### <a name="create-an-hcn-endpoint"></a>Создание конечной точки ХКН

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для создания конечной точки вычислений сети узла, а затем она добавляется в виртуальную машину или контейнер.

```C++
using unique_hcn_endpoint = wil::unique_any<
    HCN_ENDPOINT,
    decltype(&HcnCloseEndpoint),
    HcnCloseEndpoint>;

void CreateAndHotAddEndpoint()
{
    unique_hcn_endpoint hcnendpoint;
    unique_hcn_network hcnnetwork;

    wil::unique_cotaskmem_string errorRecord;


    std::wstring settings[] = LR"(
    {
        "SchemaVersion": {
            "Major": 2,
            "Minor": 0
        },
        "Owner" : "Sample",
                   "Flags" : 0,
        "HostComputeNetwork" : "87fdcf16-d210-426e-959d-2a1d4f41d6d3",
        "DNS" : {
            "Suffix" : "net.home",
            "ServerList" : "10.0.0.10",
        }
    })";
    GUID endpointGuid;
    HRESULT result = CoCreateGuid(&endpointGuid);

    result = HcnOpenNetwork(
        networkGuid,              // Unique ID
        &hcnnetwork,
        &errorRecord
        );
    if (FAILED(result))
    {
        // Failed to find network
        THROW_HR(result);
    }

    result = HcnCreateEndpoint(
        hcnnetwork.get(),
        endpointGuid,              // Unique ID
        settings.c_str(),      // Compute system settings document
        &hcnendpoint,
        &errorRecord
        );

    if (FAILED(result))
    {
        // Failed to create endpoint
        THROW_HR(result);
    }

    // Can use the sample from HCS API Spec on how to attach this endpoint
    // to the VM using AddNetworkAdapterToVm

    result = HcnCloseEndpoint(hcnendpoint.get());

    if (FAILED(result))
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }

}
```


### <a name="delete-an-endpoint"></a>Удалить конечную точку

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для удаления конечной точки вычислений для сети узла.

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value
    HRESULT hr = HcnDeleteEndpoint(endpointGuid, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


### <a name="modify-and-endpoint"></a>Изменение и конечная точка

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для изменения конечной точки вычислений для сети узла.

```C++
    unique_hcn_endpoint hcnendpoint;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value

    HRESULT hr = HcnOpenEndpoint(endpointGuid, &hcnendpoint, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    std::wstring  ModifySettingAddPortJson = LR"(
    {
        "ResourceType" : 0,
        "RequestType" : 0,
        "Settings" : {
            "PortName" : "acbd341a-ec08-44c0-9d5e-61af0ee86902"
            "VirtualNicName" : "641313e1-7ae8-4ddb-94e5-3215f3a0b218--87fdcf16-d210-426e-959d-2a1d4f41d6d1"
            "VirtualMachineId" : "641313e1-7ae8-4ddb-94e5-3215f3a0b218"
        }
    }
    )";


    hr = HcnModifyEndpoint(hcnendpoint.get(), ModifySettingAddPortJson.c_str(), &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


### <a name="enumerate-all-enpoints"></a>Перечислить все енпоинтс

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для перечисления всех конечных точек вычислений в сети узла.

```C++
    wil::unique_cotaskmem_string errorRecord;

    wil::unique_cotaskmem_string resultEndpoints;
    wil::unique_cotaskmem_string errorRecord;

    // Filter to select Endpoint based on properties
    std::wstring filter [] = LR"(
    {
        "Name"  : "sampleNetwork",
    })";
    result = HcnEnumerateEndpoints(filter.c_str(), &resultEndpoints, &errorRecord);
    if (FAILED(result))
    {
        THROW_HR(result);
    }
```


### <a name="query-endpoint-properties"></a>Свойства конечной точки запроса

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для запроса всех свойств конечной точки вычислений сети узла.

```C++
    unique_hcn_endpoint hcnendpoint;
    wil::unique_cotaskmem_string errorRecord;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value

    HRESULT hr = HcnOpenEndpoint(endpointGuid, &hcnendpoint, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }



    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    {
        // Future
    })";

    hr = HcnQueryEndpointProperties(hcnendpoint.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the errorRecord Json
        THROW_HR(hr);
    }
```


## <a name="scenario-hcn-namespace"></a>Сценарий: пространство имен ХКН

### <a name="create-an-hcn-namespace"></a>Создание пространства имен ХКН

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для создания пространства имен среды вычислений на узле, которое можно использовать для подключения конечных точек и контейнеров.

```C++
using unique_hcn_namespace = wil::unique_any<
    HCN_NAMESPACE,
    decltype(&HcnCloseNamespace),
    HcnCloseNamespace>;

/// Creates a simple HCN Network, waiting synchronously to finish the task
void CreateHcnNamespace()
{

    unique_hcn_namespace handle;
    wil::unique_cotaskmem_string errorRecord;
    std::wstring settings = LR"(
    {
        "SchemaVersion": {
            "Major": 2,
            "Minor": 0
        },
        "Owner" : "Sample",
        "Flags" : 0,
        "Type" : 0,
    })";

    GUID namespaceGuid;
    HRESULT result = CoCreateGuid(&namespaceGuid);

    result = HcnCreateNamespace(
        namespaceGuid,              // Unique ID
        settings.c_str(),      // Compute system settings document
        &handle,
        &errorRecord
        );
    if (FAILED(result))
    {
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //    "ErrorCode" : <uint32>,
        //    "Error" : <string>,
        //    "Success" : <bool>,
       //   }

        // Failed to create network
        THROW_HR(result);
    }

    result = HcnCloseNamespace(handle.get());

    if (FAILED(result))
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }

}
```


### <a name="delete-an-hcn-namespace"></a>Удаление пространства имен ХКН

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для удаления пространства имен вычислений сети узла.

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnDeleteNamespace(namespaceGuid, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }

```


### <a name="modify-an-hcn-namespace"></a>Изменение пространства имен ХКН

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для изменения пространства имен вычислений сети узла.

```C++
    unique_hcn_namespace handle;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnOpenNamespace(namespaceGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

    wil::unique_cotaskmem_string errorRecord;
    static std::wstring  ModifySettingAddEndpointJson = LR"(
    {
        "ResourceType" : 1,
        "ResourceType" : 0,
        "Settings" : {
            "EndpointId" : "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        }
    }
    )";


    hr = HcnModifyNamespace(handle.get(), ModifySettingAddEndpointJson.c_str(), &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
    hr = HcnCloseNamespace(handle.get());

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

```


### <a name="enumerate-all-namespaces"></a>Перечислить все пространства имен

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для перечисления всех пространств имен вычислений сети узла.

```C++
    wil::unique_cotaskmem_string resultNamespaces;
    wil::unique_cotaskmem_string errorRecord;

    std::wstring filter [] = LR"(
    {
            // Future
    })";
    HRESULT hr = HcnEnumerateNamespace(filter.c_str(), &resultNamespaces, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

```


### <a name="query-namespace-properties"></a>Свойства пространства имен запроса

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для запроса свойств пространства имен для среды выполнения вычислений сети сервера

```C++
    unique_hcn_namespace handle;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnOpenNamespace(namespaceGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    {
        // Future
    })";

    HRESULT hr = HcnQueryNamespaceProperties(handle.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

```


## <a name="scenario-hcn-load-balancer"></a>Сценарий: подсистема балансировки нагрузки ХКН

### <a name="create-an-hcn-load-balancer"></a>Создание балансировщика нагрузки ХКН

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для создания Load Balancer на узле, который может использоваться для балансировки нагрузки конечной точки в рамках вычислений.

```C++
using unique_hcn_loadbalancer = wil::unique_any<
    HCN_LOADBALANCER,
    decltype(&HcnCloseLoadBalancer),
    HcnCloseLoadBalancer>;

/// Creates a simple HCN LoadBalancer, waiting synchronously to finish the task
void CreateHcnLoadBalancer()
{

    unique_hcn_loadbalancer handle;
    wil::unique_cotaskmem_string errorRecord;
    std::wstring settings = LR"(
     {
        "SchemaVersion": {
            "Major": 2,
            "Minor": 0
        },
        "Owner" : "Sample",
        "HostComputeEndpoints" : [
            "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        ],
        "VirtualIPs" : [ "10.0.0.10" ],
        "PortMappings" : [
            {
                "Protocol" : 0,
                "InternalPort" : 8080,
                "ExternalPort" : 80,
            }
        ],
        "EnableDirectServerReturn" : true,
        "InternalLoadBalancer" : false,
    }
     )";

    GUID lbGuid;
    HRESULT result = CoCreateGuid(&lbGuid);


    HRESULT hr = HcnCreateLoadBalancer(
        lbGuid,              // Unique ID
        settings.c_str(),      // LoadBalancer settings document
        &handle,
        &errorRecord
        );
    if (FAILED(hr))
    {
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //    "ErrorCode" : <uint32>,
        //    "Error" : <string>,
        //    "Success" : <bool>,
       //   }

        // Failed to create network
        THROW_HR(hr);
    }

    hr = HcnCloseLoadBalancer(handle.get());

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

}
```


### <a name="delete-an-hcn-load-balancer"></a>Удаление балансировщика нагрузки ХКН

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для удаления подсистемы балансировки сетевой нагрузки.

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value
    HRESULT hr = HcnDeleteLoadBalancer(lbGuid , &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
```


### <a name="modify-an-hcn-load-balancer"></a>Изменение балансировщика нагрузки ХКН

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для изменения пространства имен вычислений сети узла.

```C++
    unique_hcn_loadbalancer handle;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value

    HRESULT hr = HcnOpenLoadBalancer(lbGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

    wil::unique_cotaskmem_string errorRecord;
    static std::wstring  ModifySettingAddEndpointJson = LR"(
    {
        "ResourceType" : 1,
        "ResourceType" : 0,
        "Settings" : {
            "EndpointId" : "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        }
    }
    )";


    hr = HcnModifyLoadBalancer(handle.get(), ModifySettingAddEndpointJson.c_str(), &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
    hr = HcnCloseLoadBalancer(handle.get());

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


### <a name="enumerate-all-load-balancers"></a>Перечисление всех подсистем балансировки нагрузки

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для перечисления всех Load Balancerных вычислений сети узла.

```C++
    wil::unique_cotaskmem_string resultLoadBalancers;
    wil::unique_cotaskmem_string errorRecord;

    std::wstring filter [] = LR"(
    {
         // Future

    })";
    HRESULT result = HcnEnumerateLoadBalancers(filter.c_str(), & resultLoadbalancers, &errorRecord);
    if (FAILED(result))
    {
            // UnMarshal  the result Json

            THROW_HR(result);
    }
```


### <a name="query-load-balancer-properties"></a>Свойства подсистемы балансировки нагрузки запросов

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений узла для запроса свойств балансировщика нагрузки сети.

```C++
    unique_hcn_loadbalancer handle;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value

    HRESULT hr = HcnOpenLoadBalancer(lbGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    {
        "ID"  : "",
        "Type" : 0,
    })";

    hr = HcnQueryNProperties(handle.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


## <a name="scenario-hcn-notifications"></a>Сценарий: уведомления ХКН

### <a name="register-and-unregister-service-wide-notifications"></a>Регистрация и Отмена регистрации уведомлений на уровне службы

В этом примере показано, как использовать API-интерфейс сетевой службы вычислений для регистрации и отмены регистрации для уведомлений на уровне службы. Это позволяет вызывающему объекту получить уведомление (через функцию обратного вызова, заданную во время регистрации) при каждом выполнении операции на уровне службы, такой как новое событие создания сети.

```C++
using unique_hcn_callback = wil::unique_any<
    HCN_CALLBACK,
    decltype(&HcnUnregisterServiceCallback),
    HcnUnregisterServiceCallback>;

// Callback handle returned by registration api. Kept at
// global or module scope as it will automatically be
// unregistered when it goes out of scope.
unique_hcn_callback g_Callback;

// Event notification callback function.
void
CALLBACK
ServiceCallback(
    DWORD   NotificationType,
    void*   Context,
    HRESULT NotificationStatus,
    PCWSTR  NotificationData)
{
    // Optional client context
    UNREFERENCED_PARAMETER(context);
    // Reserved for future use
    UNREFERENCED_PARAMETER(NotificationStatus);

    switch (NotificationType)
    {
        case HcnNotificationNetworkCreate:
            // TODO: UnMarshal the NotificationData
            //
            // // Notification
            // {
            //     "ID" : Guid,
            //     "Flags" : <uint32>,
            // };
            break;

        case HcnNotificationNetworkDelete:
            // TODO: UnMarshal the NotificationData
            break;

        Default:
            // TODO: handle other events.
            break;
    }
}

/// Register for service-wide notifications
void RegisterForServiceNotifications()
{
    THROW_IF_FAILED(HcnRegisterServiceCallback(
        ServiceCallback,
        nullptr,
        &g_Callback));
}

/// Unregister from service-wide notifications
void UnregisterForServiceNotifications()
{
    // As this is a unique_hcn_callback, this will cause HcnUnregisterServiceCallback to be invoked
    g_Callback.reset();

}
```

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения об [дескрипторах контекста RPC для хкн](hcn-declaration-handles.md).

- Дополнительные сведения о [схемах документов JSON хкн](hcn-json-document-schemas.md).