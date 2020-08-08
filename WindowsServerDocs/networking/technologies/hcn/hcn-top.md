---
title: API службы вычислений для сети (ХКН) для виртуальных машин и контейнеров
description: API службы вычислений с помощью сети (ХКН) — это общедоступный API Win32, предоставляющий доступ на уровне платформы для управления виртуальными сетями, конечными точками виртуальной сети и связанными политиками. Вместе это обеспечивает подключение и безопасность виртуальных машин и контейнеров, работающих на узле Windows.
ms.author: jmesser
author: jmesser81
ms.date: 11/05/2018
ms.openlocfilehash: 8e83af4ea54d2fcc75ff8ff054f4ad253a5422ea
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955664"
---
# <a name="host-compute-network-hcn-service-api-for-vms-and-containers"></a>API службы вычислений для сети (ХКН) для виртуальных машин и контейнеров

>Область применения: Windows Server (половина ежегодного канала), Windows Server 2019

API службы вычислений с помощью сети (ХКН) — это общедоступный API Win32, предоставляющий доступ на уровне платформы для управления виртуальными сетями, конечными точками виртуальной сети и связанными политиками. Вместе это обеспечивает подключение и безопасность виртуальных машин и контейнеров, работающих на узле Windows.

Разработчики используют API службы ХКН для управления сетями для виртуальных машин и контейнеров в рабочих процессах приложений. API ХКН был разработан для обеспечения лучшей работы для разработчиков. Конечные пользователи не взаимодействуют с этими API напрямую.

## <a name="features-of-the-hcn-service-api"></a>Функции API службы ХКН
-    Реализуется как API-интерфейс C, размещенный в сетевой службе узла (HNS) на виртуальной машине/VM.

-    Предоставляет возможность создавать, изменять, удалять и перечислять объекты ХКН, такие как сети, конечные точки, пространства имен и политики. Операции выполняются с дескрипторами объектов (например, дескриптором сети), а внутренние эти дескрипторы реализуются с помощью дескрипторов контекста RPC.

-    На основе схемы. Большинство функций API определяют входные и выходные параметры как строки, содержащие аргументы вызова функции как документы JSON. Документы JSON основаны на строго типизированных и версий схемах, эти схемы являются частью общедоступной документации.

-    API подписки или обратного вызова позволяет клиентам регистрироваться для получения уведомлений о событиях уровня службы, таких как создание и удаление сети.

-    API ХКН работает в классическом Bridge ( Centennial) — приложения, работающие в системных службах. API проверяет список ACL, получая маркер пользователя от вызывающего.

>[!TIP]
>API службы ХКН поддерживается в фоновых задачах и в окнах без переднего плана.

## <a name="terminology-host-vs-compute"></a>Терминология: размещение и вычисление
Служба вычислений узлов позволяет вызывающим объектам создавать виртуальные машины и контейнеры на одном физическом компьютере и управлять ими. Он назван для соблюдения отраслевых терминологии.

- **Узел** широко используется в отрасли виртуализации для обращения к операционной системе, предоставляющей виртуализованные ресурсы.

- **Вычисление** используется для обращения к методам виртуализации, которые являются более широкими, чем просто виртуальные машины. Служба вычислительной сети узла позволяет вызывающим объектам создавать и управлять сетью как для виртуальных машин, так и для контейнеров на одном физическом компьютере.

## <a name="schema-based-configuration-documents"></a>Документы конфигурации на основе схемы
Документы конфигурации, основанные на четко определенных схемах, — это установленный промышленный стандарт в пространстве виртуализации. Большинство решений виртуализации, таких как DOCKER и Kubernetes, предоставляют интерфейсы API на основе документов конфигурации. Некоторые отраслевые инициативы, в которых участвует Корпорация Майкрософт, управляют экосистемой для определения и проверки этих схем, например [OpenAPI](https://www.openapis.org/).  Эти инициативы также управляют стандартизацией определенных определений схемы для схем, используемых для контейнеров, таких как [открытая инициатива по созданию контейнеров (OCI)](https://www.opencontainers.org/).

Язык, используемый для создания документов конфигурации, — это [JSON](https://tools.ietf.org/html/rfc8259), который используется в сочетании с:
-    Определения схемы, определяющие объектную модель для документа
-    Проверка того, соответствует ли документ JSON схеме
-    Автоматическое преобразование документов JSON в собственные представления этих схем и обратно в языках программирования, используемых вызывающими объектами API

Часто используемые определения схемы — это [OpenAPI](https://www.openapis.org/) и [схема JSON](http://json-schema.org/), которые позволяют указать подробные определения свойств в документе, например:
-    Допустимый набор значений для свойства, например 0-100 для свойства, представляющего процент.
-    Определение перечислений, представленных в виде набора допустимых строк для свойства.
-    Регулярное выражение для ожидаемого формата строки.

В процессе документирования API-интерфейсов ХКН мы планируем опубликовать схему документов JSON как спецификацию OpenAPI. Основываясь на этой спецификации, характерные для конкретного языка представления схемы могут обеспечить строго типизированное использование объектов схемы на языке программирования, используемом клиентом.

### <a name="example"></a>Пример

Ниже приведен пример этого рабочего процесса для объекта, представляющего контроллер SCSI в документе конфигурации виртуальной машины.

```
enum IpamType
{
    [NewIn("2.0")] Static,
    [NewIn("2.0")] Dhcp,
};

class Ipam
{
    // Type : dhcp
    [NewIn("2.0"),OmitEmpty] IpamType   Type;
    [NewIn("2.0"),OmitEmpty] Subnet     Subnets[];
};

class Subnet : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] string         IpAddressPrefix;
    [NewIn("2.0"),OmitEmpty] SubnetPolicy   Policies[];
    [NewIn("2.0"),OmitEmpty] Route          Routes[];
};


enum SubnetPolicyType
{
    [NewIn("2.0")] VLAN
};

class SubnetPolicy
{
    [NewIn("2.0"),OmitEmpty] SubnetPolicyType                 Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Common.PolicySettings Data;
};

class PolicySettings
{
    [NewIn("2.0"),OmitEmpty]  string      Name;
};

class VlanPolicy : HCN.Schema.Common.PolicySettings
{
    [NewIn("2.0")] uint32 IsolationId;
};

class Route
{
    [NewIn("2.0"),OmitEmpty] string NextHop;
    [NewIn("2.0"),OmitEmpty] string DestinationPrefix;
    [NewIn("2.0"),OmitEmpty] uint16 Metric;
};

```

>[!TIP]
>Заметки [Невин ("2.0") являются частью поддержки управления версиями для определений схемы.

Из этого внутреннего определения мы создаем спецификации OpenAPI для схемы:

```
{
    "swagger" : "2.0",
    "info" : {
       "version" : "2.1",
       "title" : "HCN API"
    },
    "definitions": {
        "Ipam": {
            "type": "object",
            "properties": {
                "Type": {
                    "type": "string",
                    "enum": [
                        "Static",
                        "Dhcp"
                    ],
                    "description": " Type : dhcp"
                },
                "Subnets": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/Subnet"
                    }
                }
            }
        },
        "Subnet": {
            "type": "object",
            "properties": {
                "ID": {
                    "type": "string",
                    "pattern": "^[0-9A-Fa-f]{8}-([0-9A-Fa-f]{4}-){3}[0-9A-Fa-f]{12}$"
                },
                "IpAddressPrefix": {
                    "type": "string"
                },
                "Policies": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/SubnetPolicy"
                    }
                },
                "Routes": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/Route"
                    }
                }
            }
        },
        "SubnetPolicy": {
            "type": "object",
            "properties": {
                "Type": {
                    "type": "string",
                    "enum": [
                        "VLAN",
                        "VSID"
                    ]
                },
                "Data": {
                    "$ref": "#/definitions/PolicySettings"
                }
            }
        },
        "PolicySettings": {
            "type": "object",
            "properties": {
                "Name": {
                    "type": "string"
                }
            }
        },
        "VlanPolicy": {
            "type": "object",
            "properties": {
                "Name": {
                    "type": "string"
                },
                "IsolationId": {
                    "type": "integer",
                    "format": "uint32"
                }
            }
        },
        "Route": {
            "type": "object",
            "properties": {
                "NextHop": {
                    "type": "string"
                },
                "DestinationPrefix": {
                    "type": "string"
                },
                "Metric": {
                    "type": "integer",
                    "format": "uint16"
                }
            }
        }
    }
}
```

С помощью таких средств, как [Swagger](https://swagger.io/), можно создавать представления языка программирования схемы, используемого клиентом, для конкретного языка. Swagger поддерживает различные языки, такие как C#, Go, JavaScript и Python.

- [Пример созданного кода C#](example-c-sharp.md) для объекта подсети IPAM верхнего уровня &.

- [Пример созданного кода Go](example-go.md) для объекта подсети IPAM верхнего уровня &. Go используется DOCKER и Kubernetes, которые являются двумя потребителями API-интерфейсов сетевой службы вычислений. Go имеет встроенную поддержку упаковки типов Go в документы JSON и обратно.

Помимо создания и проверки кода, можно использовать средства для упрощения работы с документами JSON, то есть [Visual Studio Code](https://code.visualstudio.com/Docs/languages/json).

### <a name="top-level-objects-defined-in-the-hcnschemasmars-file"></a>Объекты верхнего уровня, определенные в ХКН. Файл Schemas. Mars
Как упоминалось выше, схему документа для документов, используемых API-интерфейсами ХКН, можно найти в наборе файлов. Mars: onecore/VM/DV/NET/HNS/Schema/Mars/Schema.

Объекты верхнего уровня:
- [хосткомпутенетворк](hcn-scenarios.md#scenario-hcn)
- [хосткомпутиндпоинт](hcn-scenarios.md#scenario-hcn-endpoint)
- [хосткомпутенамеспаце](hcn-scenarios.md#scenario-hcn-namespace)
- [хосткомпутелоадбаланцер](hcn-scenarios.md#scenario-hcn-load-balancer)

```
class HostComputeNetwork : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.NetworkMode          Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.NetworkPolicy        Policies[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.MacPool              MacPool;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.DNS                  Dns;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Ipam                 Ipams[];
};

class HostComputeEndpoint : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] string                                     HostComputeNetwork;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Endpoint.EndpointPolicy Policies[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Endpoint.IpConfig       IpConfigurations[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.DNS                     Dns;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Route                   Routes[];
    [NewIn("2.0"),OmitEmpty] string                                     MacAddress;
};

class HostComputeNamespace : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] uint32                                    NamespaceId;
    [NewIn("2.0"),OmitEmpty] Guid                                      NamespaceGuid;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Namespace.NamespaceType        Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Namespace.NamespaceResource    Resources[];
};

class HostComputeLoadBalancer : HCN.Schema.Common.Base
{
    [NewIn("2.0"), OmitEmpty] string                                               HostComputeEndpoints[];
    [NewIn("2.0"), OmitEmpty] string                                               VirtualIPs[];
    [NewIn("2.0"), OmitEmpty] HCN.Schema.Network.Endpoint.Policy.PortMappingPolicy PortMappings[];
    [NewIn("2.0"), OmitEmpty] HCN.Schema.LoadBalancer.LoadBalancerPolicy           Policies[];
};
```

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения об [общих сценариях хкн](hcn-scenarios.md).

- Дополнительные сведения об [дескрипторах контекста RPC для хкн](hcn-declaration-handles.md).

- Дополнительные сведения о [схемах документов JSON хкн](hcn-json-document-schemas.md).
