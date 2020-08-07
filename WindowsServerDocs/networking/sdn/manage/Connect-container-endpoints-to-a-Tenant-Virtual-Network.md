---
title: Подключение конечных точек контейнера к виртуальной сети клиента
description: В этом разделе мы покажем, как подключить конечные точки контейнера к существующей виртуальной сети клиента, созданной с помощью SDN. Для создания сети контейнера на виртуальной машине клиента используется драйвер сети l2bridge (и, возможно, l2tunnel), доступный в подключаемом модуле Windows либнетворк для DOCKER.
manager: grcusanz
ms.topic: article
ms.assetid: f7af1eb6-d035-4f74-a25b-d4b7e4ea9329
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/24/2018
ms.openlocfilehash: fd05441ecc64c05778234dc00fa315bb406dfb40
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970811"
---
# <a name="connect-container-endpoints-to-a-tenant-virtual-network"></a>Подключение конечных точек контейнера к виртуальной сети клиента

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе мы покажем, как подключить конечные точки контейнера к существующей виртуальной сети клиента, созданной с помощью SDN. Для создания сети контейнера на виртуальной машине клиента используется драйвер сети *l2bridge* (и, возможно, *l2tunnel*), доступный в подключаемом модуле Windows либнетворк для DOCKER.

В разделе [драйверы сети контейнера](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/network-drivers-topologies) мы обсуждали, что несколько сетевых драйверов доступны через DOCKER в Windows. Для SDN Используйте драйверы *l2bridge* и *l2tunnel* . Для обоих драйверов каждая конечная точка контейнера находится в той же виртуальной подсети, что и виртуальная машина узла контейнера (клиента).

Сетевая служба узла (HNS) через подключаемый модуль частного облака динамически назначает IP-адреса конечным точкам контейнера. Конечные точки контейнера имеют уникальные IP-адреса, но используют один и тот же MAC-адрес виртуальной машины узла контейнера (клиента) из-за преобразования адресов второго уровня.

Политика сети (списки управления доступом, Инкапсуляция и качество обслуживания) для этих конечных точек контейнера применяется на физическом узле Hyper-V, полученном сетевым контроллером, и определяется в системах управления верхнего уровня.

Разница между драйверами *l2bridge* и *l2tunnel* :


|                                                                                                                                                                                                                                                                            l2bridge                                                                                                                                                                                                                                                                            |                                                                                                 l2tunnel                                                                                                  |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Конечные точки контейнера, которые находятся в: <ul><li>Одна и та же виртуальная машина узла контейнера и в одной подсети имеют весь сетевой трафик, включенный в виртуальный коммутатор Hyper-V. </li><li>Трафик на разных виртуальных машинах узла или в разных подсетях пересылается физическому узлу Hyper-V. </li></ul>Политика сети не применяется, так как сетевой трафик между контейнерами на одном узле и в той же подсети не передается физическому узлу. Политика сети применяется только к межузловому или сетевому трафику контейнера между подсетями. | *Весь* сетевой трафик между двумя конечными точками контейнера перенаправляется на физический узел Hyper-V независимо от узла или подсети. Политика сети применяется к сетевому трафику между подсетями и между узлами. |

---

>[!NOTE]
>Эти сетевые режимы не работают для подключения конечных точек контейнера Windows к виртуальной сети клиента в общедоступном облаке Azure.


## <a name="prerequisites"></a>Предварительные требования
-  Развернутая инфраструктура SDN с сетевым контроллером.
-  Создана виртуальная сеть клиента.
-  Развернутая виртуальная машина клиента с включенной функцией контейнеров Windows, установленным DOCKER и включенной функцией Hyper-V. Компонент Hyper-V необходим для установки нескольких двоичных файлов для сетей l2bridge и l2tunnel.

   ```powershell
   # To install HyperV feature without checks for nested virtualization
   dism /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V /All
   ```

>[!Note]
>[Вложенная виртуализация](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/nesting) и предоставление расширений виртуализации не требуются, если не используются контейнеры Hyper-V.


## <a name="workflow"></a>Рабочий процесс

[1. Добавьте несколько IP-конфигураций в существующий ресурс NIC виртуальной машины через сетевой контроллер (узел Hyper-V)](#1-add-multiple-ip-configurations) 
 [2. Включите сетевой прокси-сервер на узле, чтобы выделить IP-адреса ЦС для конечных точек контейнера (узел Hyper-V)](#2-enable-the-network-proxy) 
 [3. Установите подключаемый модуль частного облака, чтобы назначить IP-адреса ЦС конечным точкам контейнера (виртуальная машина узла контейнера)](#3-install-the-private-cloud-plug-in) 
 [4. Создание сети *l2bridge* или *l2tunnel* с помощью DOCKER (виртуальная машина узла контейнера)](#4-create-an-l2bridge-container-network)

>[!NOTE]
>В ресурсах NIC виртуальной машины, созданных с помощью System Center Virtual Machine Manager, не поддерживается несколько IP-конфигураций. Рекомендуется использовать эти типы развертываний, которые создают ресурс NIC виртуальной машины из аппаратного контроллера управления с помощью сетевого контроллера PowerShell.

### <a name="1-add-multiple-ip-configurations"></a>1. Добавление нескольких IP-конфигураций
На этом этапе предполагается, что сетевая карта виртуальной машины клиента имеет одну IP-конфигурацию с IP-адресом 192.168.1.9 и подключена к ИДЕНТИФИКАТОРу ресурса виртуальной сети "VNet1" и ресурсу виртуальной машины "Subnet1" в подсети 192.168.1.0/24 IP. Мы добавили 10 IP-адресов для контейнеров из 192.168.1.101-192.168.1.110.

```powershell
Import-Module NetworkController

# Specify Network Controller REST IP or FQDN
$uri = "<NC REST IP or FQDN>"
$vnetResourceId = "VNet1"
$vsubnetResourceId = "Subnet1"

$vmnic= Get-NetworkControllerNetworkInterface -ConnectionUri $uri | where {$_.properties.IpConfigurations.Properties.PrivateIPAddress -eq "192.168.1.9" }
$vmsubnet = Get-NetworkControllerVirtualSubnet -VirtualNetworkId $vnetResourceId -ResourceId $vsubnetResourceId -ConnectionUri $uri

# For this demo, we will assume an ACL has already been defined; any ACL can be applied here
$allowallacl = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"


foreach ($i in 1..10)
{
    $newipconfig = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
    $props = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties

    $resourceid = "IP_192_168_1_1"
    if ($i -eq 10)
    {
        $resourceid += "10"
        $ipstr = "192.168.1.110"
    }
    else
    {
        $resourceid += "0$i"
        $ipstr = "192.168.1.10$i"
    }

    $newipconfig.ResourceId = $resourceid
    $props.PrivateIPAddress = $ipstr

    $props.PrivateIPAllocationMethod = "Static"
    $props.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $props.Subnet.ResourceRef = $vmsubnet.ResourceRef
    $props.AccessControlList = new-object Microsoft.Windows.NetworkController.AccessControlList
    $props.AccessControlList.ResourceRef = $allowallacl.ResourceRef

    $newipconfig.Properties = $props
    $vmnic.Properties.IpConfigurations += $newipconfig
}

New-NetworkControllerNetworkInterface -ResourceId $vmnic.ResourceId -Properties $vmnic.Properties -ConnectionUri $uri
```

### <a name="2-enable-the-network-proxy"></a>2. Включите сетевой прокси-сервер.
На этом шаге вы включите сетевой прокси-сервер, чтобы выделить несколько IP-адресов для виртуальной машины узла контейнера.

Чтобы включить сетевой прокси-сервер, запустите сценарий [ConfigureMCNP.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/ConfigureMCNP.ps1) на **узле Hyper-V** , где размещается виртуальная машина узла контейнера (клиента).

```powershell
PS C:\> ConfigureMCNP.ps1
```

### <a name="3-install-the-private-cloud-plug-in"></a>3. Установка подключаемого модуля частного облака
На этом шаге вы установите подключаемый модуль, чтобы служба HNS могла взаимодействовать с сетевым прокси-сервером на узле Hyper-V.

Чтобы установить подключаемый модуль, запустите скрипт [InstallPrivateCloudPlugin.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/InstallPrivateCloudPlugin.ps1) в **виртуальной машине узла контейнера (клиента)**.


```powershell
PS C:\> InstallPrivateCloudPlugin.ps1
```

### <a name="4-create-an-l2bridge-container-network"></a>4. Создание сети контейнера *l2bridge*
На этом шаге вы используете `docker network create` команду на **виртуальной машине узла контейнера (клиента)** для создания сети l2bridge.

```powershell
# Create the container network
C:\> docker network create -d l2bridge --subnet="192.168.1.0/24" --gateway="192.168.1.1" MyContainerOverlayNetwork

# Attach a container to the MyContainerOverlayNetwork
C:\> docker run -it --network=MyContainerOverlayNetwork <image> <cmd>
```

>[!NOTE]
>Назначение статических IP-адресов не поддерживается для сетей контейнеров *l2bridge* или *l2tunnel* при использовании с стеком Microsoft Sdn.

## <a name="more-information"></a>Дополнительные сведения
Дополнительные сведения о развертывании инфраструктуры SDN см. [в статье Развертывание программно-определяемой сетевой инфраструктуры](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure).

