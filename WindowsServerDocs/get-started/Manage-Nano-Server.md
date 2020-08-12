---
title: Управление сервером Nano Server
description: обновления, пакеты обслуживания, сетевые трассировки, мониторинг производительности
manager: DonGill
ms.date: 09/06/2017
ms.topic: get-started-article
ms.assetid: 599d6438-a506-4d57-a0ea-1eb7ec19f46e
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 78a869f826bd9d13e627f5710cca1b3ef1cdcdc4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87959632"
---
# <a name="manage-nano-server"></a>Управление сервером Nano Server

>Область применения. Windows Server 2016

> [!IMPORTANT]
> Начиная с Windows Server версии 1709, сервер Nano Server будет доступен только в качестве [базового образа ОС контейнера](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image). Его описание см. в статье об [изменениях сервера Nano Server](nano-in-semi-annual-channel.md).

Управление Nano Server осуществляется удаленно. Эта ОС не поддерживает возможность локального входа и службы удаленных терминалов. Однако вам доступен обширный спектр возможностей для удаленного управления Nano Server, включая Windows PowerShell, инструментарий управления Windows (WMI) и удаленное управление Windows и службы аварийного управления (EMS).

Чтобы использовать любое средство удаленного управления, возможно, потребуется знать IP-адрес сервера Nano Server. Ниже перечислено несколько способов для определения IP-адреса:

-   Используйте агент восстановления Nano (дополнительные сведения см. в разделе "Использование агента восстановления Nano Server" этой статьи).

-   Подключите к компьютеру последовательный кабель и используйте EMS.

-   Используя имя компьютера, назначенное Nano Server во время настройки, можно получить IP-адрес с помощью средства ping. Например, `ping NanoServer-PC /4`.

## <a name="using-windows-powershell-remoting"></a>Использование удаленного взаимодействия Windows PowerShell
Для управления сервером Nano Server с помощью удаленного взаимодействия Windows PowerShell вам следует добавить IP-адрес сервера Nano Server в список доверенных узлов на компьютере управления, добавить учетную запись, которую вы используете, в группу администраторов сервера Nano Server и включить CredSSP, если вы планируете использовать эту функцию.

> [!NOTE]
> Если целевой сервер Nano Server и ваш компьютер управления находятся в одном лесу доменных служб Active Directory (или в лесах с отношением доверия), не следует добавлять сервер Nano Server в список доверенных узлов, так как вы можете подключиться к серверу, используя его полное доменное имя, например: PS C:\> Enter-PSSession -ComputerName nanoserver.contoso.com -Credential (Get-Credential)


Чтобы добавить сервер Nano Server в список доверенных узлов, выполните следующую команду в командной строке Windows PowerShell с повышенными привилегиями:

`Set-Item WSMan:\localhost\Client\TrustedHosts <IP address of Nano Server>`

Чтобы запустить удаленный сеанс Windows PowerShell, запустите локальный сеанс Windows PowerShell с повышенными привилегиями и выполните следующие команды:


```
$ip = <IP address of Nano Server>
$user = $ip\Administrator
Enter-PSSession -ComputerName $ip -Credential $user
```


Теперь вы можете выполнять команды Windows PowerShell на сервере Nano Server в обычном режиме.

> [!NOTE]
> В этом выпуске сервера Nano Server доступны не все команды Windows PowerShell. Чтобы просмотреть доступные команды, выполните команду `Get-Command -CommandType Cmdlet`.

Чтобы остановить удаленный сеанс, выполните команду `Exit-PSSession`.

## <a name="using-windows-powershell-cim-sessions-over-winrm"></a>Использование сеансов Windows PowerShell CIM через WinRM
Сеансы и экземпляры CIM можно использовать в Windows PowerShell для выполнения команд WMI через службу удаленного управления Windows (WinRM).

Запустите сеанс CIM, выполнив следующие команды в командной строке Windows PowerShell:


```
$ip = <IP address of the Nano Server\>
$user = $ip\Administrator
$cim = New-CimSession -Credential $user -ComputerName $ip
```


В рамках запущенного сеанса можно выполнять различные команды WMI, например:


```
Get-CimInstance -CimSession $cim -ClassName Win32_ComputerSystem | Format-List *
Get-CimInstance -CimSession $Cim -Query SELECT * from Win32_Process WHERE name LIKE 'p%'
```


## <a name="windows-remote-management"></a>Удаленное управление Windows
Вы можете удаленно запускать программы на сервере Nano Server с помощью службы удаленного управления Windows (WinRM). Чтобы использовать службу WinRM, сначала настройте ее и задайте кодовую страницу, выполнив следующие команды в командной строке с повышенными привилегиями:

```
winrm quickconfig
winrm set winrm/config/client @{TrustedHosts=<ip address of Nano Server>}
chcp 65001
```

Теперь вы можете удаленно выполнять команды на Nano Server. Например:

```
winrs -r:<IP address of Nano Server> -u:Administrator -p:<Nano Server administrator password> ipconfig
```

Дополнительные сведения о службе удаленного управления см. в статье [Обзор удаленного управления Windows (WinRM)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265971(v=ws.11)).



## <a name="running-a-network-trace-on-nano-server"></a>Выполнение сетевой трассировки на сервере Nano Server
 Netsh trace, Tracelog.exe и Logman.exe на сервере Nano Server недоступны. Чтобы записать сетевые пакеты, можно использовать следующие командлеты Windows PowerShell:


```
New-NetEventSession [-Name]
Add-NetEventPacketCaptureProvider -SessionName
Start-NetEventSession [-Name]
Stop-NetEventSession [-Name]
```
Эти командлеты подробно описаны в статье [Командлеты для записи пакетов сетевых событий в Windows PowerShell](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265971(v=ws.11))

## <a name="installing-servicing-packages"></a>Установка служебных пакетов
Если требуется установить служебные пакеты, используйте параметр -ServicingPackagePath (можно передать массив путей в CAB-файлы):

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -ServicingPackagePath \\path\to\kb123456.cab`

Зачастую служебные пакеты или исправления загружаются в качестве элементов базы знаний, содержащих CAB-файл. Выполните следующие действия, чтобы извлечь CAB-файл, который затем можно установить с помощью параметра -ServicingPackagePath:

1.  Скачайте служебный пакет (из соответствующей статье базы знаний или [каталога Центра обновления Майкрософт](https://catalog.update.microsoft.com/v7/site/home.aspx). Сохраните его в локальном каталоге или сетевой папке, например C:\ServicingPackages.
2.  Создайте папку, в которой будет сохранен извлеченный служебный пакет.  Например, c:\KB3157663_expanded
3.  Откройте консоль Windows PowerShell и используйте команду `Expand`, указав путь к MSU-файлу служебного пакета, включая параметр `-f:*` и путь, куда требуется извлечь служебный пакет.  Например: `Expand C:\ServicingPackages\Windows10.0-KB3157663-x64.msu -f:* C:\KB3157663_expanded`

    Извлеченные файлы должны выглядеть примерно следующим образом: C:>dir C:\KB3157663_expanded Volume in drive C is OS Volume Serial Number is B05B-CC3D

      Directory of C:\KB3157663_expanded

      19.04.2016 13:17 \<DIR>.
      19.04.2016 13:17 \<DIR>.
        04/17/2016  12:31 AM               517 Windows10.0-KB3157663-x64-pkgProperties.txt 04/17/2016  12:30 AM        93,886,347 Windows10.0-KB3157663-x64.cab 04/17/2016  12:31 AM               454 Windows10.0-KB3157663-x64.xml 04/17/2016  12:36 AM           185,818 WSUSSCAN.cab 4 File(s)     94,073,136 bytes 2 Dir(s)  328,559,427,584 bytes free
4.  Запустите `New-NanoServerImage` с параметром -ServicingPackagePath, указывающим на CAB-файл в этом каталоге, например: `New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -ServicingPackagePath C:\KB3157663_expanded\Windows10.0-KB3157663-x64.cab`

## <a name="managing-updates-in-nano-server"></a>Управление обновлениями на сервере Nano Server

Сейчас вы можете использовать поставщик Центра обновления Windows для инструментария управления Windows (WMI), чтобы найти список применимых обновлений и затем установить их частично или полностью. При использовании служб Windows Server Update Services (WSUS) можно также настроить сервер Nano Server для подключения к серверу WSUS в целях получения обновлений.

Во всех случаях сначала следует установить удаленный сеанс Windows PowerShell с сервером Nano Server. В этих примерах используйте *$sess* для сеанса. Если вы используете что-то другое, замените этот элемент.


### <a name="view-all-available-updates"></a>Просмотр всех доступных обновлений
---
Получите полный список применимых обновлений с помощью следующих команд:
```
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUpdates -Arguments @{SearchCriteria=IsInstalled=0;OnlineScan=$true}
```
**Примечание**. Если доступные обновления отсутствуют, эта команда возвращает следующую ошибку:
```
Invoke-CimMethod : A general error occurred that is not covered by a more specific error code.

At line:1 char:16

+ ... anResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUp ...

+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    + CategoryInfo          : NotSpecified: (MSFT_WUOperatio...-5b842a3dd45d)

   :CimInstance) [Invoke-CimMethod], CimException

    + FullyQualifiedErrorId : MI RESULT 1,Microsoft.Management.Infrastructure.

   CimCmdlets.InvokeCimMethodCommand
```

### <a name="install-all-available-updates"></a>Установка всех доступных обновлений
---
Вы можете обнаружить, скачать и установить **все** доступные обновления за один раз с помощью следующих команд:

```
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ApplyApplicableUpdates

Restart-Computer
```
**Примечание**. Защитник Windows будет препятствовать установке обновлений. Чтобы обойти эту проблему, удалите Защитник Windows, установите обновления и снова установите Защитник Windows. Кроме того, можно скачать обновления на другом компьютере, скопировать их на сервер Nano Server и затем применить с помощью DISM.exe.


### <a name="verify-installation-of-updates"></a>Проверка установки обновлений
---
Для получения списка установленных обновлений используйте следующие команды:
```
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUpdates -Arguments @{SearchCriteria=IsInstalled=1;OnlineScan=$true}
```

**Примечание**. Эти команды перечисляют установленные компоненты, но в их выходных данных нет непосредственного указания на установку. Если вам требуются подобные выходные данные, например, для отчета, можно запустить
```PowerShell
Get-WindowsPackage -Online
```

### <a name="using-wsus"></a>Использование служб WSUS
---
Перечисленные выше команды отправляют в Центр обновления Windows и Центр обновления Майкрософт в сети запрос на поиск и скачивание обновлений. При использовании служб WSUS можно задать разделы реестра на сервере Nano Server, чтобы использовать вместо этого сервер WSUS.

См. таблицу "Разделы реестра для параметров среды агента обновления Windows" в статье [Настройка автоматических обновлений в среде, отличной от Active Director](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708449(v=ws.10))

Следует задать по меньшей мере разделы реестра **WUServer** и **WUStatusServer**, но в зависимости от реализации служб WSUS могут потребоваться и другие значения. Эти параметры всегда можно уточнить, изучив другой экземпляр Windows Server в той же среде.

После установки этих значений для ваших служб WSUS команды в приведенном выше разделе запрашивают обновление у этого сервера и используют его в качестве источника для скачивания.

### <a name="automatic-updates"></a>Автоматическое обновление
---
Сейчас для автоматизации установки обновлений можно преобразовать описанные выше действия в локальный сценарий Windows PowerShell, а затем создать запланированную задачу для его запуска и перезапускать систему по расписанию.


## <a name="performance-and-event-monitoring-on-nano-server"></a>Мониторинг производительности и событий на сервере Nano Server
[comment]: # (Автор: Венкат Ялла (Venkat Yalla).)
Сервер Nano Server полностью поддерживает платформу [трассировки событий Windows](https://aka.ms/u2pa0i) (ETW), однако некоторые привычные средства для управления трассировкой и счетчиками производительности сейчас на нем недоступны. Тем не менее, сервер Nano Server имеет средства и командлеты для реализации наиболее распространенных сценариев анализа производительности.

Высокоуровневый рабочий процесс остается таким же, как и в любой установке Windows Server. Облегченная трассировка выполняется на целевом компьютере (Nano Server), а итоговые файлы трассировки и журналов проходят последующую обработку в автономном режиме на отдельном компьютере с применением таких средств, как [Windows Performance Analyzer](/previous-versions/windows/it-pro/windows-8.1-and-8/hh448170(v=win.10)), [анализатор сообщений](https://www.microsoft.com/download/details.aspx?id=44226) или иных.

> [!NOTE]
> Сведения о передаче файлов с помощью удаленного взаимодействия PowerShell см. в статье [Копирование файлов на сервер Nano Server и с него](https://aka.ms/nri9c8).

В следующих разделах перечислены наиболее распространенные операции по сбору данных о производительности, а также способы их выполнения на сервере Nano Server.

### <a name="query-available-event-providers"></a>Запрос доступных поставщиков событий
Средство [Windows Performance Recorder](/previous-versions/windows/it-pro/windows-8.1-and-8/hh448229(v=win.10)) предназначено для запроса поставщиков событий следующим образом:
```
wpr.exe -providers
```

Вы можете отфильтровать выходные данные по типу событий, которые представляют определенный интерес. Например:
```
PS C:\> wpr.exe -providers | select-string Storage

       595f33ea-d4af-4f4d-b4dd-9dacdd17fc6e                              : Microsoft-Windows-StorageManagement-WSP-Host
       595f7f52-c90a-4026-a125-8eb5e083f15e                              : Microsoft-Windows-StorageSpaces-Driver
       69c8ca7e-1adf-472b-ba4c-a0485986b9f6                              : Microsoft-Windows-StorageSpaces-SpaceManager
       7e58e69a-e361-4f06-b880-ad2f4b64c944                              : Microsoft-Windows-StorageManagement
       88c09888-118d-48fc-8863-e1c6d39ca4df                              : Microsoft-Windows-StorageManagement-WSP-Spaces
```

### <a name="record-traces-from-a-single-etw-provider"></a>Запись трассировок из одного поставщика трассировки событий Windows
Для этого можно использовать новые [командлеты для управления трассировкой событий](/previous-versions/windows/it-pro/windows-8.1-and-8/hh448229(v=win.10)). Ниже приведен пример рабочего процесса:

Создайте и запустите трассировку, указав имя файла для хранения событий.
```
PS C:\> New-EtwTraceSession -Name ExampleTrace -LocalFilePath c:\etrace.etl
```

Добавьте в трассировку GUID поставщика. Используйте ```wpr.exe -providers``` для преобразования имени поставщика в GUID.
```
PS C:\> wpr.exe -providers | select-string Kernel-Memory

       d1d93ef7-e1f2-4f45-9943-03d245fe6c00                              : Microsoft-Windows-Kernel-Memory

PS C:\> Add-EtwTraceProvider -Guid {d1d93ef7-e1f2-4f45-9943-03d245fe6c00} -SessionName ExampleTrace
```

Удалите трассировку — при этом сеанс трассировки останавливается, а события записываются в соответствующий файл журнала.
```
PS C:\> Remove-EtwTraceSession -Name ExampleTrace

PS C:\> dir .\etrace.etl

    Directory: C:\

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/14/2016  11:17 AM       16515072 etrace.etl
```
> [!NOTE]
> В этом примере показано добавление одного поставщика трассировки в сеанс, однако командлет ```Add-EtwTraceProvider``` можно использовать для сеанса несколько раз с разными GUID поставщика, чтобы включить трассировку из нескольких источников. Альтернативой является использование описанных ниже профилей ```wpr.exe```.

### <a name="record-traces-from-multiple-etw-providers"></a>Запись трассировки из нескольких поставщиков трассировки событий Windows
Параметр ```-profiles```[Windows Performance Recorder](/previous-versions/windows/it-pro/windows-8.1-and-8/hh448229(v=win.10)) позволяет одновременно осуществлять трассировку из разных поставщиков. Существует ряд встроенных профилей, таких как CPU, Network и DiskIO, которые можно выбрать:
```
PS C:\Users\Administrator\Documents> wpr.exe -profiles

Microsoft Windows Performance Recorder Version 10.0.14393 (CoreSystem)
Copyright (c) 2015 Microsoft Corporation. All rights reserved.

        GeneralProfile              First level triage
        CPU                         CPU usage
        DiskIO                      Disk I/O activity
        FileIO                      File I/O activity
        Registry                    Registry I/O activity
        Network                     Networking I/O activity
        Heap                        Heap usage
        Pool                        Pool usage
        VirtualAllocation           VirtualAlloc usage
        Audio                       Audio glitches
        Video                       Video glitches
        Power                       Power usage
        InternetExplorer            Internet Explorer
        EdgeBrowser                 Edge Browser
        Minifilter                  Minifilter I/O activity
        GPU                         GPU activity
        Handle                      Handle usage
        XAMLActivity                XAML activity
        HTMLActivity                HTML activity
        DesktopComposition          Desktop composition activity
        XAMLAppResponsiveness       XAML App Responsiveness analysis
        HTMLResponsiveness          HTML Responsiveness analysis
        ReferenceSet                Reference Set analysis
        ResidentSet                 Resident Set analysis
        XAMLHTMLAppMemoryAnalysis   XAML/HTML application memory analysis
        UTC                         UTC Scenarios
        DotNET                      .NET Activity
        WdfTraceLoggingProvider     WDF Driver Activity
```

Подробные инструкции по созданию пользовательских профилей см. в [документации по WPR.exe](/previous-versions/windows/it-pro/windows-8.1-and-8/hh448223(v=win.10)).

### <a name="record-etw-traces-during-operating-system-boot-time"></a>Запись трассировок событий Windows во время загрузки операционной системы
Используйте командлет ```New-AutologgerConfig``` для сбора событий во время загрузки системы. Работа с ним во многом аналогична командлету ```New-EtwTraceSession```, однако поставщики, добавленные в конфигурацию авторегистратора, будут включены только при следующей загрузке. Общий рабочий процесс выглядит следующим образом:

Сначала создайте новую конфигурацию авторегистратора.
```
PS C:\> New-AutologgerConfig -Name BootPnpLog -LocalFilePath c:\bootpnp.etl
```

Добавьте в нее поставщик трассировки событий Windows. В этом примере используется поставщик PnP ядра. Снова вызовите ```Add-EtwTraceProvider```, указав то же имя авторегистратора, но другой GUID, чтобы обеспечить сбор данных трассировки загрузки из нескольких источников.
```
Add-EtwTraceProvider -Guid {9c205a39-1250-487d-abd7-e831c6290539} -AutologgerName BootPnpLog
```

При этом сеанс трассировки событий Windows не запускается немедленно, а настраивается для запуска при следующей загрузке. После перезагрузки автоматически запускается новый сеанс трассировки событий Windows с именем конфигурации авторегистратора, при этом добавленные поставщики трассировки включены. Когда сервера Nano Server загрузился, следующая команда остановит сеанс трассировки после записи зарегистрированных событий в соответствующий файл трассировки:
```
PS C:\> Remove-EtwTraceSession -Name BootPnpLog
```

Чтобы запретить автоматическое создание другого сеанса трассировки при следующей загрузке, удалите конфигурацию авторегистратора следующим образом:
```
PS C:\> Remove-AutologgerConfig -Name BootPnpLog
```

Для сбора данных трассировок загрузки и установки на нескольких системах или на бездисковой системе рекомендуется использовать [коллекцию событий установки и загрузки](../administration/get-started-with-setup-and-boot-event-collection.md).

### <a name="capture-performance-counter-data"></a>Сбор данных счетчиков производительности
Обычно для отслеживания данных счетчиков производительности применяется графический интерфейс пользователя Perfmon.exe. На сервере Nano Server используйте эквивалентную программу для командной строки ```Typeperf.exe```. Например:

Запрос доступных счетчиков — можно отфильтровать выходные данные, чтобы легче находить нужные.
```
PS C:\> typeperf.exe -q | Select-String UDPv6

\UDPv6\Datagrams/sec
\UDPv6\Datagrams Received/sec
\UDPv6\Datagrams No Port/sec
\UDPv6\Datagrams Received Errors
\UDPv6\Datagrams Sent/sec
```

Параметры позволяют указать число попыток и интервал для сбора данных из счетчиков. В приведенном ниже примере показатель времени простоя процессора собирается 5 раз каждые 3 секунды.
```
PS C:\> typeperf.exe \Processor Information(0,0)\% Idle Time -si 3 -sc 5

(PDH-CSV 4.0),\\ns-g2\Processor Information(0,0)\% Idle Time
09/15/2016 09:20:56.002,99.982990
09/15/2016 09:20:59.002,99.469634
09/15/2016 09:21:02.003,99.990081
09/15/2016 09:21:05.003,99.990454
09/15/2016 09:21:08.003,99.998577
Exiting, please wait...
The command completed successfully.
```

Другие параметры командной строки позволяют, например, указать имена нужных счетчиков производительности в файле конфигурации, перенаправив выходные данные в файл журнала. Дополнительные сведения см. в [документации по typeperf.exe](/previous-versions/windows/it-pro/windows-xp/bb490960(v=technet.10)).

Кроме того, графический интерфейс Perfmon.exe можно использовать удаленно с целевыми объектами Nano Server. При добавлении счетчиков производительности в представление укажите целевой объект Nano Server в качестве имени компьютера вместо значения по умолчанию *<Local computer>* .

### <a name="interact-with-the-windows-event-log"></a>Взаимодействие с журналом событий Windows

Nano Server поддерживает командлет ```Get-WinEvent```, который предоставляет возможности фильтрации и запроса журналов событий Windows, как локально, так и на удаленном компьютере. Подробное описание параметров и примеры можно найти на [странице документации по Get-WinEvent](/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-5.1). Этот простой пример извлекает *ошибки*, отмеченные в журнале *System* за последние два дня.
```
PS C:\> $StartTime = (Get-Date) - (New-TimeSpan -Day 2)
PS C:\> Get-WinEvent -FilterHashTable @{LogName='System'; Level=2; StartTime=$StartTime} | select TimeCreated, Message

TimeCreated           Message
-----------           -------
9/15/2016 11:31:19 AM Task Scheduler service failed to start Task Compatibility module. Tasks may not be able to reg...
9/15/2016 11:31:16 AM The Virtualization Based Security enablement policy check at phase 6 failed with status: {File...
9/15/2016 11:31:16 AM The Virtualization Based Security enablement policy check at phase 0 failed with status: {File...
```

Nano Server также поддерживает командлет ```wevtutil.exe```, позволяющий получать сведения о журналах событий и издателях. Дополнительные сведения см. в [документации по wevtutil.exe](https://aka.ms/qvod7p).

### <a name="graphical-interface-tools"></a>Средства графического интерфейса
[Средства управления веб-серверами](https://techcommunity.microsoft.com/t5/windows-admin-center-blog/bg-p/Windows-Admin-Center-Blog) можно использовать для удаленного управления целевыми объектами Nano Server и отображения журнала событий Nano Server с помощью веб-браузера. Наконец, просмотр событий в оснастке MMC (eventvwr.msc) также можно использовать для просмотра журналов — просто откройте его на компьютере с рабочим столом и сориентируйте на удаленный Nano Server.




## <a name="using-windows-powershell-desired-state-configuration-with-nano-server"></a>Использование настройки требуемого состояния Windows PowerShell с помощью сервера Nano Server

Nano Server можно управлять как целевыми узлами с помощью настройки требуемого состояния (DSC) Windows PowerShell. Сейчас управлять узлами с сервером Nano Server с помощью DSC можно только в режиме push-уведомлений. На сервере Nano Server работают не все функции DSC.

Дополнительные сведения см. в статье [Использование DSC на сервере Nano Server](https://techcommunity.microsoft.com/t5/windows-admin-center-blog/bg-p/Windows-Admin-Center-Blog).
