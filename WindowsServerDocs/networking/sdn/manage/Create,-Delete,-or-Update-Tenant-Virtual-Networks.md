---
title: Создание, удаление или обновление виртуальной сети клиента
description: В этом разделе вы узнаете, как создавать, удалять и обновлять виртуальные сети виртуализации сети Hyper-V после развертывания программно-определяемой сети (SDN). Виртуализация сети Hyper-V помогает изолировать сети клиентов, чтобы каждая сеть клиентов была отдельной сущностью. Каждая сущность не имеет возможности перекрестного подключения, если только не настроены рабочие нагрузки общего доступа.
manager: grcusanz
ms.topic: article
ms.assetid: 6a820826-e829-4ef2-9a20-f74235f8c25b
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/24/2018
ms.openlocfilehash: 831fbaac35124d050432d4f3fbccc00b6f9b5f63
ms.sourcegitcommit: fb2ae5e6040cbe6dde3a87aee4a78b08f9a9ea7c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2021
ms.locfileid: "98716791"
---
# <a name="create-delete-or-update-tenant-virtual-networks"></a>Создание, удаление или обновление виртуальных сетей клиентов

>Применяется к: Windows Server 2019, Windows Server 2016

В этом разделе вы узнаете, как создавать, удалять и обновлять виртуальные сети виртуализации сети Hyper-V после развертывания программно-определяемой сети (SDN). Виртуализация сети Hyper-V помогает изолировать сети клиентов, чтобы каждая сеть клиентов была отдельной сущностью. Каждая сущность не имеет возможности перекрестного подключения, если только не настроены рабочие нагрузки общего доступа.

## <a name="create-a-new-virtual-network"></a>Создание виртуальной сети
Создание виртуальной сети для клиента помещает его в уникальный домен маршрутизации на узле Hyper-V. Под каждой виртуальной сетью связана по крайней мере одна виртуальная подсеть. Виртуальные подсети определяются префиксом IP и ссылаются на ранее определенный список ACL.

Ниже приведены действия по созданию новой виртуальной сети.

1. Найдите префиксы IP-адресов, из которых нужно создать виртуальные подсети.
2. Найдите сеть логического поставщика, на основе которой будет туннелся трафик клиента.
3. Создайте по крайней мере одну виртуальную подсеть для каждого префикса IP-адресов, указанного на шаге 1.
4. Используемых Добавьте ранее созданные списки ACL в виртуальные подсети или добавьте подключение шлюза для клиентов.

В следующей таблице приведены примеры идентификаторов подсетей и префиксов для двух вымышленных клиентов. У клиента Fabrikam есть две виртуальные подсети, в то время как клиент Contoso имеет три виртуальные подсети.


Имя клиента.  |ИДЕНТИФИКАТОР виртуальной подсети  |Префикс виртуальной подсети
---------|---------|---------
Fabrikam    |5001         |24.30.1.0/24
Fabrikam     |5002         | 24.30.2.0/20
Contoso    |6001         |  24.30.1.0/24
Contoso    | 6002        |  24.30.2.0/24
Contoso     | 6003        | 24.30.3.0/24

В следующем примере скрипта используются команды Windows PowerShell, экспортированные из модуля **нетворкконтроллер** для создания виртуальной сети Contoso и одной подсети:

```Powershell
import-module networkcontroller
$URI = "https://ncrest.contoso.local"

#Find the HNV Provider Logical Network

$logicalnetworks = Get-NetworkControllerLogicalNetwork -ConnectionUri $uri
foreach ($ln in $logicalnetworks) {
   if ($ln.Properties.NetworkVirtualizationEnabled -eq "True") {
      $HNVProviderLogicalNetwork = $ln
   }
}

#Find the Access Control List to user per virtual subnet

$acllist = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"

#Create the Virtual Subnet

$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet
$vsubnet.ResourceId = "Contoso_WebTier"
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties
$vsubnet.Properties.AccessControlList = $acllist
$vsubnet.Properties.AddressPrefix = "24.30.1.0/24"

#Create the Virtual Network

$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.1.0/24")
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork
$vnetproperties.Subnets = @($vsubnet)
New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -Properties $vnetproperties

```

## <a name="modify-an-existing-virtual-network"></a>Изменение существующей виртуальной сети
Для обновления существующей виртуальной подсети или сети можно использовать Windows PowerShell.

При выполнении следующего примера скрипта обновленные ресурсы просто помещаются в сетевой контроллер с тем же ИДЕНТИФИКАТОРом ресурса. Если клиент Contoso хочет добавить новую виртуальную подсеть (24.30.2.0/24) в свою виртуальную сеть, вы или администратор Contoso можете использовать следующий сценарий.

```PowerShell
$acllist = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"

$vnet = Get-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri

$vnet.properties.AddressSpace.AddressPrefixes += "24.30.2.0/24"

$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet
$vsubnet.ResourceId = "Contoso_DBTier"
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties
$vsubnet.Properties.AccessControlList = $acllist
$vsubnet.Properties.AddressPrefix = "24.30.2.0/24"

$vnet.properties.Subnets += $vsubnet

New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -properties $vnet.properties

```

## <a name="delete-a-virtual-network"></a>Удаление виртуальной сети

Для удаления виртуальной сети можно использовать Windows PowerShell.

Следующий пример Windows PowerShell удаляет виртуальную сеть клиента, выполняя HTTP-удаление на URI идентификатора ресурса.

```PowerShell
Remove-NetworkControllerVirtualNetwork -ResourceId "Contoso_Vnet1" -ConnectionUri $uri
```

