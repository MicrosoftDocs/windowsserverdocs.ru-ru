---
title: Настройка списка управления доступом для брандмауэра центра обработки данных
description: К сетевым интерфейсам можно применять определенные списки ACL.  Если в виртуальной подсети, к которой подключен сетевой интерфейс, также установлены списки ACL, то применяются оба списка ACL, а выше — списки ACL для сетевых интерфейсов.
manager: grcusanz
ms.topic: article
ms.assetid: 25f18927-a63e-44f3-b02a-81ed51933187
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/23/2018
ms.openlocfilehash: e466b84846a9180c9f438eda28aacbdab7b3f6fc
ms.sourcegitcommit: da2508fb978f2686178a08a9b5a65d7ae208da36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "100335401"
---
# <a name="configure-datacenter-firewall-access-control-lists-acls"></a>Настройка списков управления доступом к брандмауэру центра обработки данных (ACL)

>Применяется к: Windows Server 2019, Windows Server 2016

После создания ACL и назначения его виртуальной подсети может потребоваться переопределить список ACL по умолчанию в виртуальной подсети с помощью определенного списка ACL для отдельного сетевого интерфейса.  В этом случае конкретные списки управления доступом применяются непосредственно к сетевым интерфейсам, подключенным к виртуальным ЛС, а не к виртуальной сети. Если в виртуальной подсети, подключенной к сетевому интерфейсу, установлены списки управления доступом, то применяются оба списка ACL и приоритеты ACL сетевых интерфейсов, расположенные выше списков ACL виртуальной подсети.

>[!IMPORTANT]
>Если список ACL не был создан и назначен виртуальной сети, см. раздел [Использование списков управления доступом (ACL) для управления потоком сетевого трафика центра обработки данных](./use-acls-for-traffic-flow.md) для создания списка управления доступом и его назначения виртуальной подсети.

В этом разделе мы покажем, как добавить список управления доступом к сетевому интерфейсу. Мы также покажем, как удалить список ACL из сетевого интерфейса, используя Windows PowerShell и сетевой контроллер REST API.

- [Пример. Добавление ACL к сетевому интерфейсу](#example-add-an-acl-to-a-network-interface)
- [Пример. Удаление списка ACL из сетевого интерфейса с помощью Windows PowerShell и сетевого контроллера REST API](#example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api)


## <a name="example-add-an-acl-to-a-network-interface"></a>Пример. Добавление ACL к сетевому интерфейсу
В этом примере показано, как добавить список ACL в виртуальную сеть.

>[!TIP]
>Кроме того, можно добавить список управления доступом в то же время, когда вы создадите сетевой интерфейс.

1. Получите или создайте сетевой интерфейс, к которому будет добавлен ACL.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```

2. Получите или создайте список ACL, который будет добавлен к сетевому интерфейсу.

   ```PowerShell
   $acl = get-networkcontrolleraccesscontrollist -ConnectionUri $uri -resourceid "AllowAllACL"
   ```

3. Назначение ACL свойству Акцессконтроллист сетевого интерфейса

   ```PowerShell
    $nic.properties.ipconfigurations[0].properties.AccessControlList = $acl
   ```

4. Добавление сетевого интерфейса в сетевой контроллер

   ```
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```

## <a name="example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api"></a>Пример. Удаление списка ACL из сетевого интерфейса с помощью Windows PowerShell и сетевого контроллера REST API
В этом примере мы покажем, как удалить список управления доступом. При удалении ACL к сетевому интерфейсу применяется набор правил по умолчанию. Набор правил по умолчанию разрешает весь исходящий трафик, но блокирует весь входящий трафик.

>[!NOTE]
>Если вы хотите разрешить весь входящий трафик, необходимо выполнить предыдущий [Пример](#example-add-an-acl-to-a-network-interface) , чтобы добавить список управления доступом, который разрешает весь входящий и весь исходящий трафик.


1. Получите сетевой интерфейс, из которого будет удален список управления доступом.<br>
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```

2. Назначьте $NULL свойству конфигурации Акцессконтроллист.<br>
   ```PowerShell
   $nic.properties.ipconfigurations[0].properties.AccessControlList = $null
   ```

3. Добавьте объект сетевого интерфейса в сетевом контроллере.<br>
   ```PowerShell
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```