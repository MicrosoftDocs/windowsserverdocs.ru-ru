---
title: Контроль исходящего трафика в виртуальной сети
description: Фундаментальным аспектом облачных сетей монетизацию является выход из пропускной способности сети. Например, передача исходящих данных в Microsoft Azure бизнес-модель. Плата за исходящие данные взимается по общему объему данных, которые выходят за пределы центров обработки Azure через Интернет в заданном цикле выставления счетов.
manager: grcusanz
ms.topic: get-started-article
ms.author: anpaul
author: AnirbanPaul
ms.date: 10/02/2018
ms.openlocfilehash: a9e939b4a810848e91b5d2cb8e4b878bbcf56e84
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156460"
---
# <a name="egress-metering-in-a-virtual-network"></a>Измерение исходящего трафика в виртуальной сети

>Область применения: Windows Server 2019


Фундаментальный аспект облачных сетей монетизацию позволяет выставлять счета за использование пропускной способности сети. Плата за исходящие данные взимается по общему объему данных, которые выходят за пределы центра обработки данных через Интернет в заданном цикле выставления счетов.

Отслеживание исходящих данных для сетевого трафика SDN в Windows Server 2019 дает возможность предлагать показатели использования для передачи исходящего трафика. Сетевой трафик, который оставляет каждую виртуальную сеть, но остается в центре обработки данных, может относиться отдельно, чтобы его можно было исключить из расчета выставления счетов. Пакеты, привязанные к IP-адресам назначения, которые не включены в один из диапазонов неоплачиваемых адресов, учитываются как исходящие передачи исходящих данных.

## <a name="virtual-network-unbilled-address-ranges-allowlist-of-ip-ranges"></a>Диапазоны адресов, для которых не взимается виртуальная сеть (разрешенных диапазонов IP-адресов)

Вы можете найти неоплачиваемые диапазоны адресов в свойстве **унбилледаддрессранжес** существующей виртуальной сети. По умолчанию диапазоны адресов не добавляются.

   ```PowerShell
   import-module NetworkController
   $uri = "https://sdn.contoso.com"

   (Get-NetworkControllerVirtualNetwork -ConnectionURI $URI -ResourceId "VNet1").properties
   ```

Выходные данные будут выглядеть примерно так:
   ```
    AddressSpace           : Microsoft.Windows.NetworkController.AddressSpace
    DhcpOptions            :
    UnbilledAddressRanges  :
    ConfigurationState     :
    ProvisioningState      : Succeeded
    Subnets                : {21e71701-9f59-4ee5-b798-2a9d8c2762f0, 5f4758ef-9f96-40ca-a389-35c414e996cc,
                         29fe67b8-6f7b-486c-973b-8b9b987ec8b3}
    VirtualNetworkPeerings :
    EncryptionCredential   :
    LogicalNetwork         : Microsoft.Windows.NetworkController.LogicalNetwork
   ```


## <a name="example-manage-the-unbilled-address-ranges-of-a-virtual-network"></a>Пример. Управление неоплачиваемыми диапазонами адресов виртуальной сети

Вы можете управлять набором префиксов IP-подсетей, чтобы исключить из измерения исходящего трафика, задав свойство **унбилледаддрессранже** виртуальной сети.  Любой трафик, отправленный сетевыми интерфейсами в виртуальной сети с IP-адресом назначения, совпадающим с одним из префиксов, не будет включен в свойство Билледегрессбитес.

1.  Обновите свойство **унбилледаддрессранжес** , чтобы оно содержало подсети, для доступа к которым не будет выставлен счет.

    ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceID "VNet1"
    $vnet.Properties.UnbilledAddressRanges = "10.10.2.0/24,10.10.3.0/24"
    ```

    >[!TIP]
    >При добавлении нескольких IP-подсетей используйте запятую между каждой IP-подсетью.  Не включайте пробелы перед запятой или после нее.

2.  Обновите ресурс виртуальной сети с помощью измененного свойства **унбилледаддрессранжес** .

    ```PowerShell
    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "VNet1" -Properties $unbilled.Properties -PassInnerException
    ```

    Выходные данные будут выглядеть примерно так:
      ```
         Confirm
         Performing the operation 'New-NetworkControllerVirtualNetwork' on entities of type
         'Microsoft.Windows.NetworkController.VirtualNetwork' via
         'https://sdn.contoso.com/networking/v3/virtualNetworks/VNet1'. Are you sure you want to continue?
         [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y


         Tags             :
         ResourceRef      : /virtualNetworks/VNet1
         InstanceId       : 29654b0b-9091-4bed-ab01-e172225dc02d
         Etag             : W/"6970d0a3-3444-41d7-bbe4-36327968d853"
         ResourceMetadata :
         ResourceId       : VNet1
         Properties       : Microsoft.Windows.NetworkController.VirtualNetworkProperties
      ```


3. Проверьте виртуальную сеть, чтобы просмотреть настроенные **унбилледаддрессранжес**.

   ```PowerShell
   (Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceID "VNet1").properties
   ```

   Теперь выходные данные будут выглядеть примерно так:
   ```
   AddressSpace           : Microsoft.Windows.NetworkController.AddressSpace
   DhcpOptions            :
   UnbilledAddressRanges  : 10.10.2.0/24,192.168.2.0/24
   ConfigurationState     :
   ProvisioningState      : Succeeded
   Subnets                : {21e71701-9f59-4ee5-b798-2a9d8c2762f0, 5f4758ef-9f96-40ca-a389-35c414e996cc,
                        29fe67b8-6f7b-486c-973b-8b9b987ec8b3}
   VirtualNetworkPeerings :
   EncryptionCredential   :
   LogicalNetwork         : Microsoft.Windows.NetworkController.LogicalNetwork
   ```

## <a name="check-the-billed-the-unbilled-egress-usage-of-a-virtual-network"></a>Проверьте, оплачивается ли неоплачиваемая исходящая загрузка виртуальной сети.

После настройки свойства **унбилледаддрессранжес** можно проверить использование и выставление счетов за исходящий трафик каждой подсети в виртуальной сети. Исходящий трафик обновляется каждые четыре минуты с общим количеством байтов, которые выставляются из диапазона счетов и не выставляются.

Для каждой виртуальной подсети доступны следующие свойства:

-   **Унбилледегрессбитес** показывает число неоплачиваемых байтов, отправленных сетевыми интерфейсами, подключенными к этой виртуальной подсети. Неоплачиваемые байты — байты, отправляемые в диапазоны адресов, которые являются частью свойства **унбилледаддрессранжес** родительской виртуальной сети.

-   **Билледегрессбитес** показывает число байтов, выданных в счетах, отправленных сетевыми интерфейсами, подключенными к этой виртуальной подсети. Выставляемые байты — это байты, отправляемые в диапазоны адресов, которые не являются частью свойства **унбилледаддрессранжес** родительской виртуальной сети.

Используйте следующий пример для запроса исходящего использования:

```PowerShell
(Get-NetworkControllerVirtualNetwork -ConnectionURI $URI -ResourceId "VNet1").properties.subnets.properties | ft AddressPrefix,BilledEgressBytes,UnbilledEgressBytes
```

Выходные данные будут выглядеть примерно так:
```
AddressPrefix BilledEgressBytes UnbilledEgressBytes
------------- ----------------- -------------------
10.0.255.8/29          16827067                   0
10.0.2.0/24           781733019                   0
10.0.4.0/24                   0                   0
```


---
