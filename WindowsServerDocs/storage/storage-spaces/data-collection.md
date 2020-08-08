---
title: Сбор диагностических данных с помощью Локальные дисковые пространства
description: Основные сведения о средствах сбора данных Локальные дисковые пространства, а также конкретные примеры их запуска и использования.
ms.author: adagashe
ms.topic: article
author: adagashe
ms.date: 10/24/2018
ms.openlocfilehash: fa71408dbb6a4757150ee896a760f37914aacc38
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960977"
---
# <a name="collect-diagnostic-data-with-storage-spaces-direct"></a>Сбор диагностических данных с помощью Локальные дисковые пространства

> Применяется к: Windows Server 2019, Windows Server 2016

Существует несколько средств диагностики, которые можно использовать для сборов данных, необходимых для устранения неполадок Локальные дисковые пространства и отказоустойчивого кластера. В этой статье мы рассмотрим раздел **Get-сддкдиагностиЦинфо** — одно средство сенсорного ввода, которое будет собирать все важные сведения, помогающие в диагностике кластера.

Учитывая, что журналы и другие сведения, указанные в **Get-сддкдиагностиЦинфо** , сжимаются, сведения об устранении неполадок, приведенных ниже, будут полезны для устранения сложных проблем, которые были переданы в корпорацию Майкрософт для рассмотрения.

## <a name="installing-get-sddcdiagnosticinfo"></a>Установка Get-СддкдиагностиЦинфо

Командлет PowerShell **Get-сддкдиагностиЦинфо** (также **Get-пксторажедиагностиЦинфо**, ранее известный как **Test-сторажехеалс**), можно использовать для сбора журналов и выполнения проверок работоспособности для отказоустойчивой кластеризации (кластера, ресурсов, сетей, узлов), дисковых пространств (физических дисков, корпусов, виртуальных дисков), общих томов кластера, файловых ресурсов SMB и дедупликации.

Существует два способа установки сценария, оба из которых описаны ниже.

### <a name="powershell-gallery"></a>Коллекция PowerShell

[Коллекция PowerShell](https://www.powershellgallery.com/packages/PrivateCloud.DiagnosticInfo) является моментальным снимком репозитория GitHub. Обратите внимание, что для установки элементов из коллекция PowerShell требуется последняя версия модуля PowerShellGet, которая доступна в Windows 10, в Windows Management Framework (WMF) 5,0 или в установщике на основе MSI (для PowerShell 3 и 4).

Во время этого процесса мы установим последнюю версию [средств диагностики сетей Майкрософт](https://www.powershellgallery.com/packages/MSFT.Network.Diag) , так как Get-сддкдиагностиЦинфо полагается на это. Этот модуль манифеста содержит средство диагностики и устранения неполадок сети, которые поддерживаются группой продуктов Майкрософт для сетей Microsoft Core.

Вы можете установить модуль, выполнив следующую команду в PowerShell с правами администратора:

``` PowerShell
Install-PackageProvider NuGet -Force
Install-Module PrivateCloud.DiagnosticInfo -Force
Import-Module PrivateCloud.DiagnosticInfo -Force
Install-Module -Name MSFT.Network.Diag
```

Чтобы обновить модуль, выполните следующую команду в PowerShell:

``` PowerShell
Update-Module PrivateCloud.DiagnosticInfo
```

### <a name="github"></a>GitHub

[Репозиторий GitHub](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/) — это самая последняя версия модуля, так как мы постоянно выполним итерацию. Чтобы установить модуль из GitHub, скачайте последнюю версию модуля из [архива](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/archive/master.zip) и извлеките каталог PrivateCloud. диагностиЦинфо в правильный путь к модулям PowerShell, на который указывает```$env:PSModulePath```

``` PowerShell
# Allowing Tls12 and Tls11 -- e.g. github now requires Tls12
# If this is not set, the Invoke-WebRequest fails with "The request was aborted: Could not create SSL/TLS secure channel."
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$module = 'PrivateCloud.DiagnosticInfo'
Invoke-WebRequest -Uri https://github.com/PowerShell/$module/archive/master.zip -OutFile $env:TEMP\master.zip
Expand-Archive -Path $env:TEMP\master.zip -DestinationPath $env:TEMP -Force
if (Test-Path $env:SystemRoot\System32\WindowsPowerShell\v1.0\Modules\$module) {
    rm -Recurse $env:SystemRoot\System32\WindowsPowerShell\v1.0\Modules\$module -ErrorAction Stop
    Remove-Module $module -ErrorAction SilentlyContinue
} else {
    Import-Module $module -ErrorAction SilentlyContinue
}
if (-not ($m = Get-Module $module -ErrorAction SilentlyContinue)) {
    $md = "$env:ProgramFiles\WindowsPowerShell\Modules"
} else {
    $md = (gi $m.ModuleBase -ErrorAction SilentlyContinue).PsParentPath
    Remove-Module $module -ErrorAction SilentlyContinue
    rm -Recurse $m.ModuleBase -ErrorAction Stop
}
cp -Recurse $env:TEMP\$module-master\$module $md -Force -ErrorAction Stop
rm -Recurse $env:TEMP\$module-master,$env:TEMP\master.zip
Import-Module $module -Force

```

Если необходимо получить этот модуль в автономном кластере, скачайте zip-файл, переместите его на узел целевого сервера и установите модуль.

## <a name="gathering-logs"></a>Идет сбор журналов

После включения каналов событий и завершения процесса установки можно использовать командлет PowerShell Get-СддкдиагностиЦинфо в модуле, чтобы получить:

- Отчеты о работоспособности хранилища, а также сведения о неработоспособных компонентах
- Отчеты о емкости хранилища по пулам, томам и дедупликации томов
- Журналы событий со всех узлов кластера и сводный отчет об ошибках

Предположим, что у кластера хранилища есть имя *«clus01».*

Для выполнения в удаленном кластере хранилища:

``` PowerShell
Get-SDDCDiagnosticInfo -ClusterName CLUS01
```

Для локального выполнения на кластерном узле хранилища:

``` PowerShell
Get-SDDCDiagnosticInfo
```

Чтобы сохранить результаты в указанную папку, выполните следующие действия.

``` PowerShell
Get-SDDCDiagnosticInfo -WriteToPath D:\Folder
```

Ниже приведен пример того, как это выглядит в реальном кластере:

``` PowerShell
New-Item -Name SDDCDiagTemp -Path d:\ -ItemType Directory -Force
Get-SddcDiagnosticInfo -ClusterName S2D-Cluster -WriteToPath d:\SDDCDiagTemp
```

Как видите, скрипт также выполняет проверку текущего состояния кластера.

![снимок экрана PowerShell для сбора данных](media/data-collection/CollectData.png)

Как видите, все данные записываются в папку Сддкдиагтемп

![снимок экрана данных в проводнике](media/data-collection/CollectDataFolder.png)

После завершения скрипта он создаст ZIP-файл в каталоге Users.

![снимок экрана данных в PowerShell](media/data-collection/CollectDataResult.png)

Давайте создадим отчет в текстовом файле.

```PowerShell
#find the latest diagnostic zip in UserProfile
    $DiagZip=(get-childitem $env:USERPROFILE | where Name -like HealthTest*.zip)
    $LatestDiagPath=($DiagZip | sort lastwritetime | select -First 1).FullName
#expand to temp directory
    New-Item -Name SDDCDiagTemp -Path d:\ -ItemType Directory -Force
    Expand-Archive -Path $LatestDiagPath -DestinationPath D:\SDDCDiagTemp -Force
#generate report and save to text file
    $report=Show-SddcDiagnosticReport -Path D:\SDDCDiagTemp
    $report | out-file d:\SDDCReport.txt

```

Для справки ниже приведена ссылка на [образец отчета](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/SDDCReport.txt) и [Пример ZIP](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/HealthTest-S2D-Cluster-20180522-1546.ZIP)-файла.

Чтобы просмотреть это в центре администрирования Windows (начиная с версии 1812), перейдите на вкладку *Диагностика* . Как видно на снимке экрана ниже, можно

- Установка средств диагностики
- Обновите их (если они устарели),
- Запланируйте ежедневное диагностическое выполнение (это оказывает низкую нагрузку на систему, обычно занимает <5 минут в фоновом режиме и не занимают больше 500 МБ в кластере).
- Просмотрите ранее собранные диагностические сведения, если вам нужно предоставить ее для поддержки или анализа самостоятельно.

![снимок экрана системы диагностики ВАК](media/data-collection/Wac.png)

## <a name="get-sddcdiagnosticinfo-output"></a>Выходные данные Get-СддкдиагностиЦинфо

Ниже приведены файлы, входящие в сжатый вывод команды Get-СддкдиагностиЦинфо.

### <a name="health-summary-report"></a>Сводный отчет о работоспособности

Сводный отчет о работоспособности сохраняется как:
- 0_CloudHealthSummary. log

Этот файл создается после анализа всех собираемых данных и предназначен для краткой сводки системы. Она содержит следующие виртуальные машины:

- Сведения о системе
- Общие сведения о работоспособности хранилища (количество узлов, ресурсы в сети, общие тома кластера в сети, неработоспособные компоненты и т. д.)
- Сведения о неработоспособных компонентах (неработающие кластерные ресурсы, сбой или ожидание в сети)
- Сведения о встроенном по и драйвере
- Сведения о пуле, физическом диске и томе
- Производительность хранилища (собираются счетчики производительности)

Этот отчет постоянно обновляется для включения более полезной информации. Последние сведения см. в [файле сведений GitHub](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/edit/master/README.md).

### <a name="logs-and-xml-files"></a>Журналы и XML-файлы

Скрипт запускает различные скрипты сбора журналов и сохраняет выходные данные в виде XML-файлов. Мы соберем кластеры и журналы работоспособности, сведения о системе (MSInfo32), нефильтрованные журналы событий (отказоустойчивая кластеризация, диагностика DIS, Hyper-v, дисковые пространства и др.) и сведения о диагностике хранилища (Операционные журналы). Последние сведения о собираемых сведениях см. в [файле сведений GitHub (что мы собираемся)](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/blob/master/README.md#what-does-the-cmdlet-output-include).

## <a name="how-to-consume-the-xml-files-from-get-pcstoragediagnosticinfo"></a>Как использовать XML-файлы из Get-ПксторажедиагностиЦинфо
Можно использовать данные из XML-файлов, предоставленных в данных, собираемых командлетом **Get-пксторажедиагностиЦинфо** . Эти файлы содержат сведения о виртуальных дисках, физических дисках, сведения о базовом кластере и других выходных данных, связанных с PowerShell.

Чтобы просмотреть результаты этих выходных данных, откройте окно PowerShell и выполните следующие действия.

```PowerShell
ipmo storage
$d = import-clixml <filename>
$d
```

## <a name="what-to-expect-next"></a>Что следует рассчитывать дальше?
Множество улучшений и новых командлетов для анализа работоспособности системы SDDC.
Предоставьте отзыв о том, что вы хотели бы увидеть, выполнив [здесь](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/issues)проблемы с хранением. Кроме того, вы можете внести полезные изменения в сценарий, отправив запрос на [вытягивание](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/pulls).
