---
title: Использование виртуальных сетевых устройств в виртуальной сети
description: В этом разделе вы узнаете, как развертывать сетевые виртуальные устройства в виртуальных сетях клиентов. Сетевые виртуальные устройства можно добавить в сети, которые выполняют функции маршрутизации и зеркального отображения портов, определяемые пользователем.
manager: grcusanz
ms.topic: article
ms.assetid: 3c361575-1050-46f4-ac94-fa42102f83c1
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/30/2018
ms.openlocfilehash: fc263ea778209da699cc7c78fd6111f512760951
ms.sourcegitcommit: fb2ae5e6040cbe6dde3a87aee4a78b08f9a9ea7c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2021
ms.locfileid: "98716900"
---
# <a name="use-network-virtual-appliances-on-a-virtual-network"></a>Использование виртуальных сетевых устройств в виртуальной сети

>Применяется к: Windows Server 2019, Windows Server 2016

В этом разделе вы узнаете, как развертывать сетевые виртуальные устройства в виртуальных сетях клиентов. Сетевые виртуальные устройства можно добавить в сети, которые выполняют функции маршрутизации и зеркального отображения портов, определяемые пользователем.

## <a name="types-of-network-virtual-appliances"></a>Типы виртуальных сетевых устройств

Можно использовать один из двух типов виртуальных устройств:

1. **Определяемая пользователем маршрутизация** — заменяет распределенные маршрутизаторы в виртуальной сети возможностями маршрутизации виртуального устройства.  При использовании определяемой пользователем маршрутизации виртуальное устройство используется в качестве маршрутизатора между виртуальными подсетями в виртуальной сети.

2. **Зеркальное отображение портов** . весь сетевой трафик, вводимый или оставляемый отслеживаемым портом, дублируется и отправляется виртуальному устройству для анализа.


## <a name="deploying-a-network-virtual-appliance"></a>Развертывание сетевого виртуального устройства

Чтобы развернуть сетевой виртуальный модуль, необходимо сначала создать виртуальную машину, содержащую устройство, а затем подключить ее к соответствующим подсетям виртуальной сети. Дополнительные сведения см. в статьях [Создание виртуальной машины клиента и подключение к виртуальной сети клиента или VLAN](Create-a-Tenant-VM.md).

Для некоторых устройств требуется несколько виртуальных сетевых адаптеров. Как правило, один сетевой адаптер, выделенный для управления устройством, в то время как дополнительные адаптеры обрабатывают трафик.  Если устройству требуется несколько сетевых адаптеров, необходимо создать каждый сетевой интерфейс в сетевом контроллере. Необходимо также назначить идентификатор интерфейса на каждом узле для каждого из дополнительных адаптеров, наявляющихся в разных виртуальных подсетях.

После развертывания сетевого виртуального устройства можно использовать устройство для определенной маршрутизации, зеркального отображения или и того и другого.


## <a name="example-user-defined-routing"></a>Пример. определяемая пользователем маршрутизация

Для большинства сред требуются только системные маршруты, которые уже определены распределенным маршрутизатором виртуальной сети. Однако может потребоваться создать таблицу маршрутизации и добавить один или несколько маршрутов в конкретных случаях, например:

- Принудительное туннелирование для доступа к Интернету через вашу локальную сеть.
- Использование виртуальных устройств в вашей среде.

В этих сценариях необходимо создать таблицу маршрутизации и добавить определяемые пользователем маршруты к таблице. Можно использовать несколько таблиц маршрутизации, и одну и ту же таблицу маршрутизации можно связать с одной или несколькими подсетями. Каждую подсеть можно связать только с одной таблицей маршрутизации. Все виртуальные машины в подсети используют таблицу маршрутизации, связанную с подсетью.

Подсети используют системные маршруты, пока таблица маршрутизации не будет связана с подсетью. После существования ассоциации Маршрутизация выполняется на основе наибольшего соответствия префиксов (LPM) как для определяемых пользователем маршрутов, так и для системных маршрутов. Если существует несколько маршрутов с одинаковым совпадением LPM, то определяемый пользователем маршрут выбирается первым перед системным маршрутом.

**PROCEDURE**

1. Создайте свойства таблицы маршрутов, которые содержат все определяемые пользователем маршруты.<p>Системные маршруты по-прежнему применяются в соответствии с правилами, определенными выше.

   ```PowerShell
    $routetableproperties = new-object Microsoft.Windows.NetworkController.RouteTableProperties
   ```

2. Добавьте маршрут в свойства таблицы маршрутизации.<p>Любой маршрут, предназначенный для подсети 12.0.0.0/8, направляется в виртуальное устройство по адресу 192.168.1.10. Устройство должно иметь виртуальный сетевой адаптер, подключенный к виртуальной сети, с этим IP-адресом, назначенным сетевому интерфейсу.

   ```PowerShell
    $route = new-object Microsoft.Windows.NetworkController.Route
    $route.ResourceID = "0_0_0_0_0"
    $route.properties = new-object Microsoft.Windows.NetworkController.RouteProperties
    $route.properties.AddressPrefix = "0.0.0.0/0"
    $route.properties.nextHopType = "VirtualAppliance"
    $route.properties.nextHopIpAddress = "192.168.1.10"
    $routetableproperties.routes += $route
   ```
   >[!TIP]
   >Если вы хотите добавить дополнительные маршруты, повторите этот шаг для каждого маршрута, который необходимо определить.

3. Добавьте таблицу маршрутизации к сетевому контроллеру.

   ```PowerShell
    $routetable = New-NetworkControllerRouteTable -ConnectionUri $uri -ResourceId "Route1" -Properties $routetableproperties
   ```

4. Примените таблицу маршрутизации к виртуальной подсети.<p>При применении таблицы маршрутов к виртуальной подсети Первая виртуальная подсеть в Tenant1_Vnet1 сети использует таблицу маршрутов. Можно назначить таблицу маршрутов максимальному числу подсетей в виртуальной сети.

   ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
    $vnet.properties.subnets[0].properties.RouteTable = $routetable
    new-networkcontrollervirtualnetwork -connectionuri $uri -properties $vnet.properties -resourceId $vnet.resourceid
   ```

После применения таблицы маршрутизации к виртуальной сети трафик перенаправляется в виртуальное устройство. Необходимо настроить таблицу маршрутизации в виртуальном устройстве, чтобы перенаправить трафик в соответствии с вашей средой.

## <a name="example-port-mirroring"></a>Пример: зеркальное отображение портов

В этом примере вы настраиваете трафик для MyVM_Ethernet1 на зеркальную Appliance_Ethernet1.  Предполагается, что вы развернули две виртуальные машины: один в качестве устройства, а другой — виртуальную машину для мониторинга с зеркальным отображением.

Устройство должно иметь второй сетевой интерфейс для управления. После включения зеркального отображения в качестве назначения на Appliciance_Ethernet1 он больше не получает трафик, предназначенный для IP-интерфейса, настроенного там.


**PROCEDURE**

1. Получите виртуальную сеть, в которой находятся виртуальные машины.

   ```PowerShell
   $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
   ```

2. Получите сетевые интерфейсы сетевого контроллера для источника и назначения зеркального отображения.

   ```PowerShell
   $dstNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "Appliance_Ethernet1"
   $srcNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```

3. Создайте объект сервицеинсертионпропертиес, содержащий правила зеркального отображения портов, и элемент, представляющий целевой интерфейс.

   ```PowerShell
   $portmirror = [Microsoft.Windows.NetworkController.ServiceInsertionProperties]::new()
   $portMirror.Priority = 1
   ```

4. Создайте объект сервицеинсертионрулес, содержащий правила, которые должны быть сопоставлены, чтобы трафик отправлялся на устройство.<p>Правила, определенные ниже, соответствуют всему трафику, входящему и исходящему, который представляет традиционный зеркальный сервер.  Эти правила можно изменить, если вы хотите создать зеркальное отображение определенного порта или конкретных источников и назначений.

   ```PowerShell
   $portmirror.ServiceInsertionRules = [Microsoft.Windows.NetworkController.ServiceInsertionRule[]]::new(1)

   $portmirror.ServiceInsertionRules[0] = [Microsoft.Windows.NetworkController.ServiceInsertionRule]::new()
   $portmirror.ServiceInsertionRules[0].ResourceId = "Rule1"
   $portmirror.ServiceInsertionRules[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionRuleProperties]::new()

   $portmirror.ServiceInsertionRules[0].Properties.Description = "Port Mirror Rule"
   $portmirror.ServiceInsertionRules[0].Properties.Protocol = "All"
   $portmirror.ServiceInsertionRules[0].Properties.SourcePortRangeStart = "0"
   $portmirror.ServiceInsertionRules[0].Properties.SourcePortRangeEnd = "65535"
   $portmirror.ServiceInsertionRules[0].Properties.DestinationPortRangeStart = "0"
   $portmirror.ServiceInsertionRules[0].Properties.DestinationPortRangeEnd = "65535"
   $portmirror.ServiceInsertionRules[0].Properties.SourceSubnets = "*"
   $portmirror.ServiceInsertionRules[0].Properties.DestinationSubnets = "*"
   ```

5. Создайте объект сервицеинсертионелементс, который будет содержать сетевой интерфейс зеркального устройства.

   ```PowerShell
   $portmirror.ServiceInsertionElements = [Microsoft.Windows.NetworkController.ServiceInsertionElement[]]::new(1)

   $portmirror.ServiceInsertionElements[0] = [Microsoft.Windows.NetworkController.ServiceInsertionElement]::new()
   $portmirror.ServiceInsertionElements[0].ResourceId = "Element1"
   $portmirror.ServiceInsertionElements[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionElementProperties]::new()

   $portmirror.ServiceInsertionElements[0].Properties.Description = "Port Mirror Element"
   $portmirror.ServiceInsertionElements[0].Properties.NetworkInterface = $dstNic
   $portmirror.ServiceInsertionElements[0].Properties.Order = 1
   ```

6. Добавьте объект вставки службы в сетевой контроллер.<p>При выдаче этой команды весь трафик к сетевому интерфейсу устройства, указанному на предыдущем шаге, останавливается.

   ```PowerShell
   $portMirror = New-NetworkControllerServiceInsertion -ConnectionUri $uri -Properties $portmirror -ResourceId "MirrorAll"
   ```

7. Обновите сетевой интерфейс источника для зеркального отображения.

   ```PowerShell
   $srcNic.Properties.IpConfigurations[0].Properties.ServiceInsertion = $portMirror
   $srcNic = New-NetworkControllerNetworkInterface -ConnectionUri $uri  -Properties $srcNic.Properties -ResourceId $srcNic.ResourceId
   ```

После выполнения этих действий интерфейс Appliance_Ethernet1 зеркально отображает трафик из интерфейса MyVM_Ethernet1.

---