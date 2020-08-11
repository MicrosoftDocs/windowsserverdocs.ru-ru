---
title: Настройка заголовка "Рабочие ресурсы" для RDS с помощью PowerShell в Windows Server
description: Содержит описание того, как можно изменить имя рабочей области по умолчанию в Windows Server.
ms.author: helohr
ms.date: 10/26/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: 5124ce691793570f6ffa11a43975719addb89e67
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970121"
---
# <a name="customize-the-rds-title-work-resources-using-powershell-on-windows-server"></a>Настройка заголовка "Рабочие ресурсы" для RDS с помощью PowerShell в Windows Server

При использовании Windows Server для доступа к удаленным приложениям RemoteApp или рабочим столам посредством веб-доступа к удаленному рабочему столу или нового приложения "Удаленный рабочий стол" вы могли заметить, что рабочая область по умолчанию называется "Рабочие ресурсы".  Можно легко изменить этот заголовок с помощью командлетов PowerShell.

Для этого откройте новое окно PowerShell на сервере посредника подключений и импортируйте модуль RemoteDesktop с помощью следующей команды.

```powershell
    Import-Module RemoteDesktop
```

Затем используйте команду Set-RDWorkspace для изменения имени рабочей области.

```powershell
    Set-RDWorkspace [-Name] <string> [-ConnectionBroker <string>]  [<CommonParameters>]
```

Например, можно использовать следующую команду для изменения имени рабочей области на "Contoso RemoteApps".

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker broker01.contoso.com
```

Если вы используете несколько посредников подключений в режиме высокой доступности, эту команду необходимо выполнить для активного посредника. Можно использовать приведенную ниже команду.

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker (Get-RDConnectionBrokerHighAvailability).ActiveManagementServer
```

Дополнительные сведения о командлете Set-RDWorkspace см. в справочных материалах по [Set-RDWorkspace](/powershell/module/remotedesktop/set-rdworkspace?view=win10-ps).
