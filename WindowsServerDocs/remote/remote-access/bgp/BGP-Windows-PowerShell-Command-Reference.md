---
title: Справочник по командам BGP для Windows PowerShell
description: Этот раздел можно использовать в качестве справочной документации при написании сценариев Windows PowerShell в Windows Server 2016 для добавления, настройки и удаления возможностей BGP из шлюза RAS и маршрутизаторов локальной сети удаленного доступа (LAN).
manager: brianlic
ms.topic: article
ms.assetid: 4b0240a3-b927-4a1e-b241-5f8f29a9552f
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: c59b40e81f6bb5de5031d5b2ef259c97226a7209
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950090"
---
# <a name="bgp-windows-powershell-command-reference"></a>Справочник по командам BGP для Windows PowerShell

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

Этот раздел можно использовать в качестве справочной документации при написании сценариев Windows PowerShell для добавления, настройки и удаления возможностей BGP из шлюза RAS и маршрутизаторов локальной сети удаленного доступа (LAN).

Эти команды BGP входят в набор команд Windows PowerShell для удаленного доступа для Windows Server 2016. Этот раздел поможет быстро находить команды BGP, которые нужно использовать в скриптах.

Дополнительные сведения обо всех командах удаленного доступа см. в разделе [Командлеты удаленного доступа](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11)).

## <a name="bgp-command-reference"></a>Справочник по командам BGP
В следующих разделах приводятся имя команды, назначение и синтаксис для каждой команды BGP, а также ссылка на команду в справочнике по удаленному доступу, в которой содержатся более подробные сведения о каждой команде.

Этот справочный материал содержит следующие разделы.

-   [Добавление команд](#bkmk_add)

-   [Очистить команды](#bkmk_clear)

-   [Отключение и включение команд](#bkmk_disable)

-   [Получение команд](#bkmk_get)

-   [Команды установки](#bkmk_install)

-   [Удалить команды](#bkmk_remove)

-   [Команды Set](#bkmk_set)

-   [Команды запуска и завершения](#bkmk_start)

-   [Команды удаления](#bkmk_uninstall)

### <a name="add-commands"></a><a name="bkmk_add"></a>Добавление команд
Ниже приведены команды BGP Add.

[Add-Бгпкустомрауте](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Добавляет пользовательские маршруты в таблицу маршрутизации BGP.

```
Add-BgpCustomRoute [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-Interface <String[]> ] [-Network <String[]> ] [-PassThru] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Add-BgpPeer](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Добавляет новый узел BGP.

```
Add-BgpPeer [-Name] <String> -LocalIPAddress <IPAddress> -PeerASN <UInt32> -PeerIPAddress <IPAddress> [-CimSession <CimSession[]> ] [-HoldTimeSec <UInt16> ] [-IdleHoldTimeSec <UInt16> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-LocalASN <UInt32> ] [-MaxAllowedPrefix <UInt32> ] [-OperationMode <OperationMode> {Mixed | Server} ] [-PassThru] [-PeeringMode <PeeringMode> {Automatic | Manual} ] [-RouteReflectorClient <Boolean> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Weight <UInt16> ] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Add-Бгпраутеаггрегате](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Добавляет новый статистический маршрут для конкретных маршрутов BGP.

```
Add-BgpRouteAggregate -Prefix <String> [-AttributePolicy <String[]> ] [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-PreserveASPath <PreserveASPath> ] [-RoutingDomain <String> ] [-SummaryOnly <SummaryOnly> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Add-Бгпраутер](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Добавляет маршрутизатор BGP для указанного идентификатора клиента.

```
Add-BgpRouter -BgpIdentifier <IPAddress> -LocalASN <UInt32> [-CimSession <CimSession[]> ] [-ClientToClientReflection <ClientToClientReflection> ] [-ClusterId <UInt32> ] [-CompareMEDAcrossASN <Boolean> ] [-DefaultGatewayRouting <Boolean> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-IPv6Routing <IPv6RoutingState> {Disabled | Enabled} ] [-LocalIPv6Address <IPAddress> ] [-PassThru] [-RouteReflector <RouteReflector> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-TransitRouting <TransitRouting> ] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Add-Бгпраутингполици](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Добавляет политику маршрутизации BGP в хранилище политик.

```
Add-BgpRoutingPolicy [-Name] <String> [-PolicyType] <PolicyType> {Deny | Allow | ModifyAttribute} [-AddCommunity <String[]> ] [-CimSession <CimSession[]> ] [-ClearMED] [-Force] [-IgnorePrefix <String[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MatchASNRange <UInt32[]> ] [-MatchCommunity <String[]> ] [-MatchNextHop <IPAddress[]> ] [-MatchPrefix <String[]> ] [-NewLocalPref <UInt32]> ] [-NewMED <UInt32]> ] [-NewNextHop <IPAddress> ] [-PassThru] [-RemoveAllCommunities] [-RemoveCommunity <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Add-Бгпраутингполицифорпир](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Добавляет политики маршрутизации BGP к одноранговым узлам BGP.

```
Add-BgpRoutingPolicyForPeer -Direction <PolicyDirection> {Ingress | Egress} -PolicyName <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

### <a name="clear-commands"></a><a name="bkmk_clear"></a>Очистить команды
Ниже приведены команды Clear для BGP.

[Clear-Бгпраутефлапдампенинг](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Очищает сведения о ослаблении колыханий маршрута для указанного набора маршрутов BGP.

```
Clear-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

### <a name="disable-and-enable-commands"></a><a name="bkmk_disable"></a>Отключение и включение команд
Ниже приведены команды Disable и Enable для BGP.

[Disable-Бгпраутефлапдампенинг](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Отключает ослабление маршрута для маршрутов BGP неустойчивый.

```
Disable-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Enable-Бгпраутефлапдампенинг](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Включает ослабление маршрута для маршрутов BGP неустойчивый.

```
Enable-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

### <a name="get-commands"></a><a name="bkmk_get"></a>Получение команд
Ниже приведены команды Get для BGP.

[Get-Бгпкустомрауте](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Получает настраиваемые сведения о маршруте от маршрутизатора BGP.

```
Get-BgpCustomRoute [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Get-BgpPeer](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Возвращает сведения о конфигурации для узлов BGP.

```
Get-BgpPeer [[-Name] <String[]> ] [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Get-Бгпраутеаггрегате](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Возвращает все сводные маршруты BGP, настроенные администратором.

```
Get-BgpRouteAggregate [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Get-Бгпраутефлапдампенинг](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Извлекает конфигурацию подсистемы ослабления маршрута BGP.

```
Get-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Get-Бгпраутеинформатион](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Получает сведения о маршруте BGP для одного или нескольких префиксов сети из таблицы маршрутизации BGP.

```
Get-BgpRouteInformation [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Network <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Type <RouteType> ] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Get-Бгпраутер](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Возвращает сведения о конфигурации маршрутизаторов BGP.

```
Get-BgpRouter [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String[]> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Get-Бгпраутингполици](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Возвращает сведения о конфигурации политик маршрутизации BGP.

```
Get-BgpRoutingPolicy [[-Name] <String[]> ] [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PolicyType <PolicyType> {Deny | Allow | ModifyAttribute} ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Get-Бгпстатистикс](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Извлекает связанное с пирингом BGP сообщение и статистику объявлений маршрутов.

```
Get-BgpStatistics [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]
```

### <a name="install-commands"></a><a name="bkmk_install"></a>Команды установки
Ниже приведены команды установки для шлюза RAS и BGP.

[Install-RemoteAccess](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Выполняет проверки готовности для DirectAccess (DA), чтобы убедиться, что он может быть установлен, устанавливает DA для удаленного доступа (RA) (включая управление удаленными клиентами) или только для управления удаленными клиентами, устанавливает VPN (VPN удаленного доступа и VPN типа "сеть-сеть") и устанавливает маршрутизацию BGP.

```
Parameter Set: MultiTenant
Install-RemoteAccess [-MultiTenancy] [-CapacityKbps <UInt64> ] [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MsgAuthenticator <String> {Enabled | Disabled} ] [-PassThru] [-RadiusPort <UInt16> ] [-RadiusScore <Byte> ] [-RadiusServer <String> ] [-RadiusTimeout <UInt32> ] [-SharedSecret <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]

Parameter Set: Vpn
Install-RemoteAccess [-VpnType] <String> {Vpn | VpnS2S | SstpProxy | RoutingOnly} [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-EntrypointName <String> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-IPAddressRange <String[]> ] [-IPv6Prefix <String> ] [-Legacy] [-MsgAuthenticator <String> {Enabled | Disabled} ] [-PassThru] [-RadiusPort <UInt16> ] [-RadiusScore <Byte> ] [-RadiusServer <String> ] [-RadiusTimeout <UInt32> ] [-SharedSecret <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

> [!IMPORTANT]
> При установке шлюза RAS в многоклиентский режим необходимо указать, включен ли протокол BGP для каждого клиента с помощью команды Windows PowerShell **Enable-ремотеакцессраутингдомаин** с параметром **-Type** со значением **ALL**. В следующем примере кода показано, как установить RAS в режиме многоадресной рассылки со всеми компонентами удаленного доступа (VPN-подключение типа "точка — сеть", VPN-подключением типа "сеть — сеть" и маршрутизацией BGP) для двух клиентов, Contoso и Fabrikam.

```
$Contoso_RoutingDomain = "ContosoTenant"
$Fabrikam_RoutingDomain = "FabrikamTenant"

Install-RemoteAccess -MultiTenancy

Enable-RemoteAccessRoutingDomain -Name $Contoso_RoutingDomain -Type All -PassThru
Enable-RemoteAccessRoutingDomain -Name $Fabrikam_RoutingDomain -Type All -PassThru
```

Если вы используете удаленный доступ в качестве маршрутизатора локальной сети, а не шлюза, вы по-прежнему можете использовать BGP, который предоставляет преимущества динамической маршрутизации в интрасети. Чтобы установить удаленный доступ в качестве маршрутизатора локальной сети BGP, введите следующую команду в командной строке Windows PowerShell и нажмите клавишу ВВОД.

```
Install-RemoteAccess -VpnType RoutingOnly
```

### <a name="remove-commands"></a><a name="bkmk_remove"></a>Удалить команды
Ниже приведены команды Remove для BGP.

[Remove-Бгпкустомрауте](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Удаляет настраиваемые маршруты из маршрутизатора BGP.

```
Remove-BgpCustomRoute [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-Interface <String[]> ] [-Network <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Remove-BgpPeer](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Удаляет узлы BGP с маршрутизатора.

```
Remove-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Remove-Бгпраутеаггрегате](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Удаляет набор указанных статистических маршрутов BGP.

```
Remove-BgpRouteAggregate [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Remove-Бгпраутер](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Удаляет маршрутизатор BGP.

```
Remove-BgpRouter [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String[]> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Remove-Бгпраутингполици](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Удаляет политики маршрутизации из хранилища политик.

```
Remove-BgpRoutingPolicy [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Remove-Бгпраутингполицифорпир](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Удаляет политики маршрутизации с узлов BGP.

```
Parameter Set: Remove1
Remove-BgpRoutingPolicyForPeer [-CimSession <CimSession[]> ] [-Direction <PolicyDirection> {Ingress | Egress} ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-PolicyName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

### <a name="set-commands"></a><a name="bkmk_set"></a>Команды Set
Ниже приведены команды Set для BGP.

[Set-BgpPeer](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Обновляет конфигурацию указанного узла BGP.

```
Set-BgpPeer [-Name] <String> [-CimSession <CimSession[]> ] [-ClearPrefixLimit] [-Force] [-HoldTimeSec <UInt16> ] [-IdleHoldTimeSec <UInt16> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-LocalASN <UInt32> ] [-LocalIPAddress <IPAddress> ] [-MaxAllowedPrefix <UInt32> ] [-OperationMode <OperationMode> {Mixed | Server} ] [-PassThru] [-PeerASN <UInt32> ] [-PeeringMode <PeeringMode> {Automatic | Manual} ] [-PeerIPAddress <IPAddress> ] [-RouteReflectorClient <Boolean> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Weight <UInt16> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Set-Бгпраутеаггрегате](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Обновляет свойства указанного статистического маршрута BGP.

```
Set-BgpRouteAggregate -Prefix <String> [-AttributePolicy <String[]> ] [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-PreserveASPath <PreserveASPath> ] [-RoutingDomain <String> ] [-SummaryOnly <SummaryOnly> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Set-Бгпраутефлапдампенинг](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Настраивает подсистему ослабления маршрута BGP.

```
Set-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-HalfLife <UInt32> ] [-HalfLifeUnreachable <UInt32> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-MaxSuppressTime <UInt32> ] [-PassThru] [-ReuseThreshold <UInt32> ] [-RoutingDomain <String> ] [-SuppressThreshold <UInt32> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Set-Бгпраутер](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Обновляет конфигурацию локального маршрутизатора BGP для указанного идентификатора клиента.

```
Set-BgpRouter [-BgpIdentifier <IPAddress> ] [-CimSession <CimSession[]> ] [-ClientToClientReflection <ClientToClientReflection> ] [-ClusterId <UInt32> ] [-CompareMEDAcrossASN <Boolean> ] [-DefaultGatewayRouting <Boolean> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-IPv6Routing <IPv6RoutingState> {Disabled | Enabled} ] [-LocalASN <UInt32> ] [-LocalIPv6Address <IPAddress> ] [-PassThru] [-RouteReflector <RouteReflector> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-TransitRouting <TransitRouting> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Set-Бгпраутингполици](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Изменяет конфигурацию политики маршрутизации.

```
Set-BgpRoutingPolicy [-Name] <String> [-AddCommunity <String[]> ] [-CimSession <CimSession[]> ] [-ClearMED] [-Force] [-IgnorePrefix <String[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MatchASNRange <UInt32[]> ] [-MatchCommunity <String[]> ] [-MatchNextHop <IPAddress[]> ] [-MatchPrefix <String[]> ] [-NewLocalPref <UInt32]> ] [-NewMED <UInt32]> ] [-NewNextHop <IPAddress> ] [-PassThru] [-PolicyType <PolicyType> {Deny | Allow | ModifyAttribute} ] [-RemoveAllCommunities] [-RemoveCommunity <String[]> ] [-RemovePolicyClause <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

[Set-Бгпраутингполицифорпир](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Изменяет политики маршрутизации BGP для узлов BGP.

```
Set-BgpRoutingPolicyForPeer -Direction <PolicyDirection> {Ingress | Egress} -PolicyName <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

### <a name="start-and-stop-commands"></a><a name="bkmk_start"></a>Команды запуска и завершения
Ниже приведены команды запуска и завершения для BGP.

[Start-BgpPeer](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Запускает маршрутизацию сеансов для узлов BGP.

```
Start-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]
```

[BgpPeer](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Останавливает маршрутизацию сеансов для узлов BGP.

```
Stop-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

### <a name="uninstall-commands"></a><a name="bkmk_uninstall"></a>Команды удаления
Ниже приведены команды удаления для шлюза RAS и BGP.

[Uninstall-RemoteAccess](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11))

Удаляет удаленный доступ с компьютера, включая все компоненты и функции удаленного доступа (шлюз RAS, BGP и т. д.).

```
Uninstall-RemoteAccess [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-EntrypointName <String> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-ThrottleLimit <Int32> ] [-VpnType <String> {Vpn | VpnS2S} ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]
```

