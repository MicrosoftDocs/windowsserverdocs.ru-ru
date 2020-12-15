---
title: Изменение порта прослушивания в удаленном рабочем столе
description: Узнайте, как изменить порт прослушивания для клиента удаленного рабочего стола.
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: c2ace6e153b50ccf366359c70c63cf73676975ec
ms.sourcegitcommit: f86366371ed566526da211daee4e5c83eb6e37b3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/08/2020
ms.locfileid: "96843092"
---
# <a name="change-the-listening-port-for-remote-desktop-on-your-computer"></a>Изменение порта прослушивания для удаленного рабочего стола на компьютере

> Применяется к: Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2008 R2

При подключении компьютера (клиентской версии Windows или Windows Server) с помощью клиента удаленного рабочего стола функции удаленного рабочего стола на компьютере "слышат" запрос на соединение через заданный порт прослушивания (по умолчанию — 3389). Этот порт прослушивания на компьютерах Windows можно изменить путем изменения реестра.

1. Откройте редактор реестра. (В поле поиска введите "regedit").
2. Перейдите к следующему разделу реестра: **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp**
3. Найдите параметр **PortNumber**.
4. Нажмите кнопку **Редактировать > Изменить**, а затем выберите пункт **Десятичное**.
5. Введите новый номер порта, а затем нажмите кнопку **ОК**. 
6. Закройте редактор реестра и перезагрузите компьютер.

При очередном подключении компьютера к этому компьютеру с помощью удаленного рабочего стола необходимо будет ввести новый номер порта. Если вы используете брандмауэр, убедитесь, что в нем разрешены подключения к новому номеру порта.


Номер текущего порта можно проверить с помощью следующей команды PowerShell:

```powershell
Get-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "PortNumber"
```

Пример:

```powershell
PortNumber   : 3389
PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations
PSChildName  : RDP-Tcp
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
```

Номер порта RDP можно изменить с помощью следующей команды PowerShell. В этой команде укажите новый порт RDP **3390**.


Чтобы добавить новый порт RDP в реестр, выполните следующую команду:

```powershell
Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "PortNumber" -Value 3390
New-NetFirewallRule -DisplayName 'RDPPORTLatest' -Profile 'Public' -Direction Inbound -Action Allow -Protocol TCP -LocalPort 3390
```
