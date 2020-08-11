---
title: Разработка командлетов PowerShell для сервера Nano Server
description: перенос CIM, командлеты .NET, C++
manager: DonGill
ms.topic: article
ms.assetid: 7b4267f0-1c91-4a40-9262-5daf4659f686
author: jaimeo
ms.author: jaimeo
ms.date: 09/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac5bca1a054581bc89c7d8f241e4be1f89db50d0
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990649"
---
# <a name="developing-powershell-cmdlets-for-nano-server"></a>Разработка командлетов PowerShell для сервера Nano Server

>Область применения. Windows Server 2016

> [!IMPORTANT]
> Начиная с Windows Server версии 1709, сервер Nano Server будет доступен только в качестве [базового образа ОС контейнера](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image). Его описание см. в статье об [изменениях сервера Nano Server](nano-in-semi-annual-channel.md).

## <a name="overview"></a>Обзор
По умолчанию сервер Nano Server включает PowerShell Core во все установки Nano Server. PowerShell Core — это сокращенный выпуск PowerShell, который основан на .NET Core и выполняется в сокращенных выпусках Windows, таких как Nano Server и Windows IoT Core. PowerShell Core работает точно так же, как другие выпуски PowerShell, такие как Windows PowerShell в Windows Server 2016. Однако сокращенный размер Nano Server означает, что в PowerShell Core на базе Nano Server доступны не все возможности Windows Server 2016.

Если вы располагаете командлетами PowerShell, которые требуется запустить на сервере Nano Server, или разрабатываете новые командлеты для этой цели, советы и рекомендации в этом разделе помогут упростить эту задачу.

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


## <a name="installing-nano-server"></a>Установка сервера Nano Server
Краткие и подробные шаги по установке сервера Nano Server на виртуальных машинах или физических компьютерах приведены в разделе [Установка сервера Nano Server](Getting-Started-with-Nano-Server.md), который является родительским по отношению к данному.

> [!NOTE]
> Для разработки на базе сервера Nano Server может оказаться полезным установить сервер Nano Server с использованием параметра -Development в New-NanoServerImage. Это позволит устанавливать неподписанные драйверы, копировать двоичные файлы отладчика, открыть порт для отладки, включить тестовую подпись и установку пакетов AppX без лицензии разработчика. Например:
>
>`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -Development`

## <a name="determining-the-type-of-cmdlet-implementation"></a>Определение типа реализации командлета
PowerShell поддерживает несколько типов реализации для командлетов, которые определяют, какие средства и процедуры используются в процессе создания или переноса для работы на сервере Nano Server. Ниже приведены поддерживаемые типы реализации:
* CIM — состоит из файлов CDXML, наложенных на поставщиков CIM (WMI версии 2)
* .NET — состоит из сборок .NET, которые реализуют управляемые интерфейсы командлетов, обычно написанные на языке C.
* Сценарий PowerShell — состоит из модулей сценариев (psm1) или сценариев (ps1), написанных на языке PowerShell

Если вы не знаете, какую реализацию вы использовали для существующих командлетов, которые требуется перенести, установите продукт или компонент и найдите папку модуля PowerShell в одном из следующих расположений:

* %windir%\system32\WindowsPowerShell\v1.0\Modules
* %ProgramFiles%\WindowsPowerShell\Modules
* %UserProfile%\Documents\WindowsPowerShell\Modules
* \<your product installation location>

  Проверьте эти расположения на соответствие следующим условиям:
  * Командлеты CIM имеют расширения файла CDXML.
  * Командлеты .NET имеют расширения файла DLL или сборки, установленные в глобальном кэше сборок, который указан в PSD1-файле в поле RootModule, ModuleToProcess или NestedModules.
* Командлеты сценария PowerShell имеют расширения файлов PSM1 или PS1.

## <a name="porting-cim-cmdlets"></a>Перенос командлетов CIM
В общем случае эти командлеты должны работать в Nano Server без обязательного преобразования. Однако следует перенести базовый поставщик WMI версии 2 для запуска на сервере Nano Server, если это еще не было сделано.

### <a name="building-c-for-nano-server"></a>Создание кода C++ для Nano Server
Чтобы получить библиотеки DLL на языке C++, работающие на Nano Server, скомпилируйте их для Nano Server, а не для конкретного выпуска.

Необходимые условия и пошаговое руководство по разработке на C++ для Nano Server см. в статье [Разработка собственных приложений на базе сервера Nano Server](/archive/blogs/nanoserver/developing-native-apps-on-nano-server).


## <a name="porting-net-cmdlets"></a>Перенос командлетов .NET
На сервере Nano Server поддерживается большая часть кода C#. Для поиска несовместимых API можно использовать [ApiPort](https://github.com/Microsoft/dotnet-apiport).

### <a name="powershell-core-sdk"></a>Пакет SDK для Powershell Core
В [коллекции PowerShell](https://www.powershellgallery.com/packages/Microsoft.PowerShell.NanoServer.SDK/) присутствует модуль Microsoft.PowerShell.NanoServer.SDK. Он упрощает разработку командлетов .NET с помощью Visual Studio 2015 с обновлением 2, которые предназначены для версий CoreCLR и PowerShell Core, доступных в Nano Server. Вы можете установить модуль, используя PowerShellGet со следующей командой:

`Find-Module Microsoft.PowerShell.NanoServer.SDK -Repository PSGallery | Install-Module -Scope <scope>`

Модуль SDK для PowerShell Core предоставляет командлеты для настройки правильных ссылочных сборок CoreCLR и PowerShell Core, создания в Visual Studio 2015 проекта на C#, предназначенного для этих ссылочных сборок, и настройки удаленного отладчика на компьютере Nano Server, чтобы разработчики могли удаленно выполнять отладку своих командлетов .NET на сервере Nano Server в Visual Studio 2015.

Модулю SDK для PowerShell Core требуется Visual Studio 2015 с обновлением 2. Если у вас не установлена среда Visual Studio 2015, можно установить [Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx).

Работа модуля SDK также зависит от наличия следующих компонентов в Visual Studio 2015:

- Разработка приложений для Windows и веб-приложений -> Средства разработки универсальных приложений Windows -> Средства (1.3.1) и Windows 10 SDK

Проверьте установку Visual Studio перед использованием модуля SDK, чтобы убедиться в соблюдении этих условий. Обязательно выберите установку указанного выше компонента во время установки Visual Studio или измените существующий экземпляр Visual Studio 2015, чтобы установить этот компонент.

Модуль SDK PowerShell Core включает в себя следующие командлеты:
- New-NanoCSharpProject: создает проект C# Visual Studio, ориентированный на CoreCLR и PowerShell Core, входящие в выпуск Windows Server 2016 для Nano Server.
- Show-SdkSetupReadMe: переходит в корневую папку SDK в проводнике и открывает файл README.txt для настройки вручную.
- Install-RemoteDebugger: устанавливает и настраивает удаленный отладчик Visual Studio на компьютере Nano Server.
- Start-RemoteDebugger: запускает удаленный отладчик на удаленном компьютере под управлением Nano Server.
- Stop-RemoteDebugger: останавливает удаленный отладчик на удаленном компьютере под управлением Nano Server.

Чтобы получить подробные сведения об использовании этих командлетов, выполните команду Get-Help для каждого командлета после установки и импорта модуля следующим образом:

`Get-Command -Module Microsoft.PowerShell.NanoServer.SDK | Get-Help -Full`


### <a name="searching-for-compatible-apis"></a>Поиск совместимых API

Вы можете выполнить поиск в каталоге API для .NET Core или дизассемблировать ссылочные сборки среды CLR Core. Дополнительные сведения о переносимости платформы для API .NET см. в статье [Переносимость платформы](https://github.com/Microsoft/dotnet-apiport/blob/master/docs/HowTo/PlatformPortability.md).

### <a name="pinvoke"></a>PInvoke
В среде CLR Core, используемой Nano Server, некоторые основополагающие библиотеки DLL, такие как kernel32.dll и advapi32.dll, были разделены на множество наборов API, поэтому вам потребуется убедиться, что вызовы PInvoke ссылаются на правильный API. Любая несовместимость проявится как ошибка во время выполнения.

Список собственных API, поддерживаемых на сервере Nano Server, см. в статье [API сервера Nano Server](/previous-versions/windows/desktop/legacy/mt588480(v=vs.85)).

### <a name="building-c-for-nano-server"></a>Создание кода C# для Nano Server

После создания в Visual Studio 2015 проекта C# с помощью `New-NanoCSharpProject` можно легко собрать его, выбрав меню **Сборка** и **Собрать проект** или **Собрать решение**. Созданные сборки будут ориентированы на правильные CoreCLR и PowerShell Core, поставляемые вместе с Nano Server, и можно просто скопировать эти сборки на компьютер под управлением Nano Server и использовать их.

### <a name="building-managed-c-cppcli-for-nano-server"></a>Создание управляемого кода C++ (CPP/CLI) для Nano Server
Управляемый код C++ не поддерживается для CoreCLR. При переносе в CoreCLR перепишите управляемый код C++ в C# и выполните все собственные вызовы через PInvoke.

## <a name="porting-powershell-script-cmdlets"></a>Перенос командлетов сценариев PowerShell

PowerShell Core имеет полное языковое соответствие PowerShell с другими выпусками PowerShell, включая выпуск для Windows Server 2016 и Windows 10. Однако при переносе командлетов сценариев PowerShell на сервер Nano Server необходимо учитывать следующие факторы:
* Существуют ли зависимости от других командлетов? Если это так, доступны ли эти командлеты на сервере Nano Server? В статье [PowerShell на сервере Nano Server](PowerShell-on-Nano-Server.md) приведены сведения о недоступных компонентах.
* Если имеются зависимости от сборок, загружаемых во время выполнения, продолжат ли они работать?
* Как можно выполнить отладку сценария удаленно?
* Как можно выполнить миграцию из WMI .Net в MI .Net?

### <a name="dependency-on-built-in-cmdlets"></a>Зависимость от встроенных командлетов
Не все командлеты в Windows Server 2016 доступны на сервере Nano Server (см. статью [PowerShell на сервере Nano Server](PowerShell-on-Nano-Server.md)). Лучше всего настроить виртуальную машину с Nano Server и выяснить, доступны ли нужные командлеты. Для этого запустите `Enter-PSSession` для подключения к целевому серверу Nano Server, а затем `Get-Command -CommandType Cmdlet, Function` для получения списка доступных командлетов.

### <a name="consider-using-powershell-classes"></a>Возможность использования классов PowerShell
Add-Type поддерживается на сервере Nano Server для компиляции встроенного кода C#. Если вы пишете новый код или переносите существующий, можно использовать классы PowerShell для определения пользовательских типов. Вы можете использовать классы PowerShell для сценариев контейнера свойств, а также для перечислений. Если необходимо выполнить PInvoke, сделайте это через C# с помощью Add-Type или в предварительно скомпилированной сборке.
Ниже приведен пример использования Add-Type:

```
Add-Type -ReferencedAssemblies ([Microsoft.Management.Infrastructure.Ciminstance].Assembly.Location) -TypeDefinition @'
public class TestNetConnectionResult
{
   // The compute name
   public string ComputerName = null;
   // The Remote IP address used for connectivity
   public System.Net.IPAddress RemoteAddress = null;
}
'@
# Create object and set properties
$result = New-Object TestNetConnectionResult
$result.ComputerName = Foo
$result.RemoteAddress = 1.1.1.1

```
 В этом примере показано использование классов PowerShell на сервере Nano Server:

```
class TestNetConnectionResult
{
   # The compute name
  [string] $ComputerName

  #The Remote IP address used for connectivity
  [System.Net.IPAddress] $RemoteAddress
}
# Create object and set properties
$result = [TestNetConnectionResult]::new()
$result.ComputerName = Foo
$result.RemoteAddress = 1.1.1.1

```

### <a name="remotely-debugging-scripts"></a>Удаленная отладка сценариев

Для удаленной отладки сценария подключитесь к удаленному компьютеру, воспользовавшись `Enter-PSsession` из интегрированной среды сценариев PowerShell. Внутри сеанса можно запустить `psedit <file_path>`, после чего копия файла открывается в локальной интегрированной среде сценариев PowerShell. Затем можно отлаживать скрипт, как если бы он выполнялся локально, задавая точки останова. Кроме того, любые изменения, внесенные в этот файл, сохраняются в удаленной версии.

### <a name="migrating-from-wmi-net-to-mi-net"></a>Переход с WMI .NET на MI .NET

[WMI .NET](/dotnet/api/?view=netframework-4.7.1) не поддерживается, поэтому все командлеты, использующие старый API, необходимо перенести на поддерживаемый API WMI: [MI. NET](/previous-versions/dn387184(v=vs.85)). Доступ к MI .NET осуществляется напрямую из C# или с помощью командлетов в модуле CimCmdlets.

### <a name="cimcmdlets-module"></a>Модуль CimCmdlets

Командлеты WMI версии 1 (например, Get-WmiObject) не поддерживаются на сервере Nano Server. Однако поддерживаются командлеты CIM (например, Get-CimInstance) в модуле CimCmdlets. Командлеты CIM очень близко соответствуют командлетам WMI версии 1. Например, Get-WmiObject похож на Get-CimInstance, так как использует схожие параметры. Синтаксис вызова метода немного отличается, но хорошо документирован посредством Invoke-CimMethod. Будьте внимательны при вводе параметров. MI .NET предъявляет более строгие требования в отношении типов параметров метода.

### <a name="c-api"></a>API C#

WMI .NET упаковывает интерфейс WMI версии 1, хотя MI .NET упаковывает интерфейс WMI версии 2 (CIM). Предоставляемые классы могут отличаться, но базовые операции очень похожи. Вы перечисляете или возвращаете экземпляры объектов и вызываете операции для них, чтобы выполнить поставленные задачи.


