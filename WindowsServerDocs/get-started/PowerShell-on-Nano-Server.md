---
title: PowerShell на сервере Nano Server
description: Различия в сокращенном наборе возможностей PowerShell на сервере Nano Server
manager: DonGill
ms.topic: article
ms.assetid: 9b25b939-1e2c-4bed-a8d3-2a8e8e46b53d
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.date: 08/07/2020
ms.openlocfilehash: 08ea28459ae58673c0c0e61310cb4bd4adcda675
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97942710"
---
# <a name="powershell-on-nano-server"></a>PowerShell на сервере Nano Server

> Область применения. Windows Server 2016

> [!IMPORTANT]
> Начиная с Windows Server версии 1709, сервер Nano Server будет доступен только в качестве [базового образа ОС контейнера](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image). Его описание см. в статье об [изменениях сервера Nano Server](nano-in-semi-annual-channel.md).

## <a name="powershell-editions"></a>Выпуски PowerShell

Начиная с версии 5.1, среда PowerShell доступна в разных выпусках, обладающих различными наборами функций и совместимостью с платформами.

- **Выпуск Desktop** создан на базе платформы .NET Framework и обеспечивает совместимость со скриптами и модулями, предназначенными для версий PowerShell в полноценных выпусках Windows, таких как Server Core и Windows Desktop.
- **Выпуск Core** создан на базе платформы .NET Framework и обеспечивает совместимость со скриптами и модулями, предназначенными для версий PowerShell в сокращенных выпусках Windows, таких как Nano Server и Windows IoT.

Запущенный выпуск PowerShell указан в свойстве PSEdition объекта $PSVersionTable.
```powershell
$PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.1.14300.1000
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
CLRVersion                     4.0.30319.42000
BuildVersion                   10.0.14300.1000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

Авторы модулей могут объявить их как совместимые с одним или более выпусками PowerShell с помощью ключа манифеста модуля CompatiblePSEditions. Этот ключ поддерживается только в PowerShell 5.1 или более поздней версии.
```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$moduleInfo = Test-ModuleManifest -Path \TestModuleWithEdition.psd1
$moduleInfo.CompatiblePSEditions
Desktop
Core

$moduleInfo | Get-Member CompatiblePSEditions

   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}

```
При получении списка доступных модулей можно отфильтровать его по выпуску PowerShell.
```powershell
Get-Module -ListAvailable | ? CompatiblePSEditions -Contains Desktop

    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions

Get-Module -ListAvailable | ? CompatiblePSEditions -Contains Core | % CompatiblePSEditions
Desktop
Core

```
Авторы сценариев могут запретить их выполнение, когда они запускаются в несовместимом выпуске PowerShell, с помощью параметра PSEdition инструкции #requires.
```powershell
Set-Content C:\script.ps1 -Value #requires -PSEdition Core
Get-Process -Name PowerShell
Get-Content C:\script.ps1
#requires -PSEdition Core
Get-Process -Name PowerShell

C:\script.ps1
C:\script.ps1 : The script 'script.ps1' cannot be run because it contained a #requires statement for PowerShell editions 'Core'. The edition of PowerShell that is required by the script does not match the currently running PowerShell Desktop edition.
At line:1 char:1
+ C:\script.ps1
+ ~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (script.ps1:String) [], RuntimeException
    + FullyQualifiedErrorId : ScriptRequiresUnmatchedPSEdition
```

## <a name="differences-in-powershell-on-nano-server"></a>Отличия в PowerShell для Nano Server
По умолчанию сервер Nano Server включает PowerShell Core во все установки Nano Server. PowerShell Core — это сокращенный выпуск PowerShell, который основан на .NET Core и выполняется в сокращенных выпусках Windows, таких как Nano Server и Windows IoT Core. PowerShell Core работает точно так же, как другие выпуски PowerShell, такие как Windows PowerShell в Windows Server 2016. Однако сокращенный размер Nano Server означает, что в PowerShell Core на базе Nano Server доступны не все возможности Windows Server 2016.


**Функции Windows PowerShell, недоступные в Nano Server**
* Адаптеры типов ADSI, ADO и WMI
* Enable-PSRemoting, Disable-PSRemoting (удаленное взаимодействие PowerShell включено по умолчанию; см. раздел "Использование удаленного взаимодействия Windows PowerShell" статьи [Установка сервера Nano Server](Getting-Started-with-Nano-Server.md)).
* Запланированные задания и модуль PSScheduledJob
* Командлеты Computer для присоединения к домену { Add | Remove } (другие способы присоединения сервера Nano Server к домену см. в разделе "Присоединение Nano Server к домену" статьи [Установка сервера Nano Server](Getting-Started-with-Nano-Server.md)).
* Reset-ComputerMachinePassword, Test-ComputerSecureChannel
* Профили (можно добавить сценарий запуска для входящих удаленных соединений с помощью `Set-PSSessionConfiguration`)
* Командлеты Clipboard
* Командлеты EventLog { Clear | Get | Limit | New | Remove | Show | Write } (используйте вместо них командлеты New-WinEvent и Get-WinEvent).
* Командлет Get-PfxCertificate
* Командлеты TraceSource { Get | Set }
* Командлеты Counter { Get | Export | Import }
* Некоторые командлеты, связанные с веб-технологиями { New-WebServiceProxy, Send-MailMessage, ConvertTo-Html }
* Ведение журнала и трассировка с помощью модуля PSDiagnostics
* Get-HotFix (сведения о получении обновлений на сервере Nano Server и управлении ими см. в статье [Управление сервером Nano Server](Manage-Nano-Server.md)).
* Командлеты неявного удаленного взаимодействия {Export-PSSession | Import-PSSession}
* New-PSTransportOption
* Транзакции PowerShell и командлеты Transaction { Complete | Get | Start | Undo | Use }
* Инфраструктура, модули и командлеты рабочего процесса PowerShell
* Out-Printer
* Update-List
* Командлеты инструментария управления Windows (WMI) версии 1: Get-WmiObject, Invoke-WmiMethod, Register-WmiEvent, Remove-WmiObject, Set-WmiInstance (используйте вместо них модуль CimCmdlets).

## <a name="using-windows-powershell-desired-state-configuration-with-nano-server"></a>Использование настройки требуемого состояния Windows PowerShell с помощью сервера Nano Server

Nano Server можно управлять как целевыми узлами с помощью настройки требуемого состояния (DSC) Windows PowerShell. Сейчас управлять узлами с сервером Nano Server с помощью DSC можно только в режиме push-уведомлений. На сервере Nano Server работают не все функции DSC.

Дополнительные сведения см. в статье [Использование DSC на сервере Nano Server](/powershell/scripting/dsc/getting-started/nanodsc).
