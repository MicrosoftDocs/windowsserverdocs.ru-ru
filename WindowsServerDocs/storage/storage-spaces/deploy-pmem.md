---
title: Общие сведения о постоянной памяти и ее развертывании
description: Подробные сведения о том, что такое постоянная память и как ее настроить с помощью локальных дисковых пространств в Windows Server 2019.
ms.author: adagashe
ms.topic: article
author: adagashe
ms.date: 1/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: 512b53be7af89fe9e0fd017af14425264062ed29
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960907"
---
# <a name="understand-and-deploy-persistent-memory"></a>Общие сведения о постоянной памяти и ее развертывании

> Область применения: Windows Server 2019

Постоянная память (или PMem) — это новый тип технологии памяти, обеспечивающий уникальную комбинацию доступной большой емкости и сохраняемости. Эта статья содержит сведения о PMem и действиях по его развертыванию в Windows Server 2019 с помощью Локальные дисковые пространства.

## <a name="background"></a>Историческая справка

PMem — это тип энергонезависимого ОЗУ (NVDIMM), сохраняющий его содержимое через циклы электропитания. Содержимое памяти остается даже при отключении питания системы в случае неожиданной потери питания, инициирования пользователем завершения работы, сбоя системы и т. д. Такая уникальная характеристика означает, что можно также использовать PMem в качестве хранилища. Именно поэтому вы можете слышать людей, которые ссылаются на PMem как на память класса хранилища.

Чтобы увидеть некоторые из этих преимуществ, давайте взглянем на следующую демонстрацию от Microsoft Ignite 2018.

[![Демонстрация Microsoft Ignite 2018 pMem](http://img.youtube.com/vi/8WMXkMLJORc/0.jpg)](http://www.youtube.com/watch?v=8WMXkMLJORc)

Любая система хранения, обеспечивающая отказоустойчивость, обязательно создает распределенные копии операций записи. Такие операции должны пройти по сети и повысить эффективность внутренний трафик записи. По этой причине абсолютные значения производительности операций ввода-вывода в секунду обычно достигаются за счет измерения только для чтения, особенно если в системе хранения используются стандартные оптимизации для чтения из локальной копии, когда это возможно. Для этого оптимизирован Локальные дисковые пространства.

**При измерении с использованием только операций чтения кластер доставляет 13 798 674 операций ввода-вывода в секунду.**

![снимок экрана 13.7 m записи операций ввода-вывода](media/deploy-pmem/iops-record.png)

При внимательном просмотре видео вы заметите, что еще более жав — задержка. Даже при более чем 13,7 м в секунду, файловая система в Windows сообщает о задержке, которая постоянно меньше 40 μс! (Это символ в микросекундах, одна миллионная доля секунды.) Эта скорость является последовательностью более быстрой, чем распространенные поставщики Flash, которые в настоящее время объявляются сегодня.

Вместе Локальные дисковые пространства в Windows Server 2019 и &reg; &trade; энергонезависимой памяти контроллера домена Intel оптане обеспечивают рекордную производительность. Этот ХЦИный тест производительности более 13.7 M операций ввода-вывода, сопровождаемый прогнозируемой и крайне низкой задержкой, является более чем удвоенным предыдущим, ведущим в отрасли показателями производительности 6.7 M операций ввода-вывода в секунду. Более того, на этот раз нам потребовалось всего 12 узлов серверов на &mdash; 25% менее двух лет назад.

![Выигрыш в операциях ввода-вывода](media/deploy-pmem/iops-gains.png)

Тестовый аппаратный контроллер — это 12-серверный кластер, который настроен для использования трех и разделенных томов ReFS, **12** x Intel &reg; S2600WFT, **384 гиб** памяти, 2 x 28-core "каскаделаке", **1,5 ТБ** памяти intel &reg; оптане &trade; DC в качестве кэша, **32 ТБ** NVMe (4 x 8 ТБ Intel &reg; DC P4510) в качестве емкости, **2** x Mellanox ConnectX-4 25 Гбит/с.

В следующей таблице приведены полные показатели производительности.

| Тест производительности                   | Производительность         |
|-----------------------------|---------------------|
| 4 КБ 100% случайное чтение         | 13 800 000 операций ввода-вывода   |
| 4 КБ 90/10% произвольное чтение/запись | 9 450 000 операций ввода-вывода   |
| последовательное чтение 2 МБ         | пропускная способность 549 ГБ/с |

### <a name="supported-hardware"></a>Поддерживаемое оборудование

В следующей таблице показано поддерживаемое оборудование энергонезависимой памяти для Windows Server 2019 и Windows Server 2016.

| Технология энергоустойчивой памяти                                      | Windows Server 2016 | Windows Server 2019 |
|-------------------------------------------------------------------|--------------------------|--------------------------|
| **NVDIMM-N** в постоянном режиме                                  | Поддерживается                | Поддерживается                |
| **Intel оптане &trade; Постоянная память контроллера домена** в режиме Direct приложения             | Не поддерживается            | Поддерживается                |
| **Intel оптане &trade; Постоянная память контроллера домена** в режиме памяти | Поддерживается            | Поддерживается                |

> [!NOTE]
> Intel Оптане поддерживает режимы *памяти* (volatile) и *Direct* (постоянные) приложения.

> [!NOTE]
> При перезагрузке системы с несколькими &reg; модулями Intel оптане &trade; PMem в режиме Direct, разделенных на несколько пространств имен, вы можете потерять доступ к некоторым или всем связанным дискам логического хранилища. Эта проблема возникает в версиях Windows Server 2019, предшествующих версии 1903.
>
> Такая утрата доступа происходит потому, что модуль PMem не обучен или завершается ошибкой при запуске системы. В этом случае все пространства имен хранилища в любом модуле PMem в системе завершатся сбоем, включая пространства имен, которые физически не соответствуют модулю, в котором произошел сбой.
>
> Чтобы восстановить доступ ко всем пространствам имен, замените неисправный модуль.
>
> Если модуль завершается сбоем в Windows Server 2019 версии 1903 или более поздней, вы теряете доступ только к тем пространствам имен, которые физически соответствуют затронутому модулю. Другие пространства имен не затрагиваются.

Теперь давайте рассмотрим настройку энергонезависимой памяти.

## <a name="interleaved-sets"></a>Наборы с чередованием

### <a name="understanding-interleaved-sets"></a>Основные сведения о чередующихся наборах

Вспомним, что устройство NVDIMM находится в стандартном гнезде DIMM (памяти), который помещает данные ближе к процессору. Эта конфигурация сокращает задержку и повышает производительность при извлечении. Чтобы повысить пропускную способность, два или более Нвдиммс создают n-направленный чередующийся набор операций чтения и записи. Наиболее распространенные конфигурации являются двусторонними или четырьмя-двусторонними. Набор с чередованием также делает несколько устройств энергонезависимой памяти одним логическим диском для Windows Server. Вы можете использовать командлет **Get-Пмемдиск** Windows PowerShell для просмотра конфигурации таких логических дисков следующим образом.

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

Как видите, логический диск PMem #2 использует физические устройства Id20 и Id120, а логический диск PMem #3 использует физические устройства Id1020 и Id1120.

Чтобы получить дополнительные сведения о наборе с чередованием, который используется логическим диском, выполните командлет **Get-пмемфисикалдевице** :

```PowerShell
(Get-PmemDisk)[0] | Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
```

### <a name="configuring-interleaved-sets"></a>Настройка чередующихся наборов

Чтобы настроить набор с чередованием, начните с просмотра всех областей постоянного объема памяти, которые не назначены логическому диску PMem в системе. Для этого выполните следующий командлет PowerShell:

```PowerShell
Get-PmemUnusedRegion

RegionId TotalSizeInBytes DeviceId
-------- ---------------- --------
       1     270582939648 {20, 120}
       3     270582939648 {1020, 1120}
```

Чтобы просмотреть все сведения об устройстве PMem в системе, включая тип устройства, расположение, работоспособность и рабочее состояние, и т. д., выполните следующий командлет на локальном сервере:

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile
                                                                                                                      memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

Так как у нас есть доступный неиспользуемый регион PMem, можно создать новые диски энергонезависимой памяти. Можно использовать неиспользуемый регион для создания нескольких дисковых накопителей с энергонезависимой памятью, выполнив следующие командлеты:

```PowerShell
Get-PmemUnusedRegion | New-PmemDisk
Creating new persistent memory disk. This may take a few moments.
```

После этого результаты можно увидеть, выполнив следующую команду:

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

Стоит отметить, что можно выполнить **Get-физический диск | Где MediaType-EQ SCM** вместо **Get-пмемдиск** для получения тех же результатов. Недавно созданный диск PMem соответствует дискам, которые отображаются в PowerShell и в центре администрирования Windows.

### <a name="using-persistent-memory-for-cache-or-capacity"></a>Использование энергонезависимой памяти для кэша или емкости

Локальные дисковые пространства в Windows Server 2019 поддерживает использование постоянной памяти в качестве диска кэша или емкости. Дополнительные сведения о настройке дисков кэша и емкости см. в разделе [Основные сведения о кэше в Локальные дисковые пространства](understand-the-cache.md).

## <a name="creating-a-dax-volume"></a>Создание тома DAX

### <a name="understanding-dax"></a>Основные сведения об DAX

Существует два способа доступа к энергонезависимой памяти. К ним относятся:

1. **Прямой доступ (DAX)**, который действует как память для получения наименьшей задержки. Приложение непосредственно изменяет постоянную память, минуя стек. Обратите внимание, что DAX можно использовать только в сочетании с NTFS.
1. **Блокировать доступ**, который действует как хранилище для совместимости приложений. В этом a данные проходят через стек. Эту конфигурацию можно использовать в сочетании с NTFS и ReFS.

На следующем рисунке показан пример конфигурации DAX:

![Стек DAX](media/deploy-pmem/dax.png)

### <a name="configuring-dax"></a>Настройка DAX

Чтобы создать том DAX на диске энергонезависимой памяти, необходимо использовать командлеты PowerShell. С помощью параметра **-исдакс** можно отформатировать том, чтобы он был включен в режим DAX.

```PowerShell
Format-Volume -IsDax:$true
```

Приведенный ниже фрагмент кода помогает создать том DAX на диске энергонезависимой памяти.

```PowerShell
# Here we use the first pmem disk to create the volume as an example
$disk = (Get-PmemDisk)[0] | Get-PhysicalDisk | Get-Disk
# Initialize the disk to GPT if it is not initialized
If ($disk.partitionstyle -eq "RAW") {$disk | Initialize-Disk -PartitionStyle GPT}
# Create a partition with drive letter 'S' (can use any available drive letter)
$disk | New-Partition -DriveLetter S -UseMaximumSize


   DiskPath: \\?\scmld#ven_8980&dev_097a&subsys_89804151&rev_0018#3&1b1819f6&0&03018089fb63494db728d8418b3cbbf549997891#{53f56307-b6
bf-11d0-94f2-00a0c91efb8b}

PartitionNumber  DriveLetter Offset                                               Size Type
---------------  ----------- ------                                               ---- ----
2                S           16777216                                        251.98 GB Basic

# Format the volume with drive letter 'S' to DAX Volume
Format-Volume -FileSystem NTFS -IsDax:$true -DriveLetter S

DriveLetter FriendlyName FileSystemType DriveType HealthStatus OperationalStatus SizeRemaining      Size
----------- ------------ -------------- --------- ------------ ----------------- -------------      ----
S                        NTFS           Fixed     Healthy      OK                    251.91 GB 251.98 GB

# Verify the volume is DAX enabled
Get-Partition -DriveLetter S | fl


UniqueId             : {00000000-0000-0000-0000-000100000000}SCMLD\VEN_8980&DEV_097A&SUBSYS_89804151&REV_0018\3&1B1819F6&0&03018089F
                       B63494DB728D8418B3CBBF549997891:WIN-8KGI228ULGA
AccessPaths          : {S:\, \\?\Volume{cf468ffa-ae17-4139-a575-717547d4df09}\}
DiskNumber           : 2
DiskPath             : \\?\scmld#ven_8980&dev_097a&subsys_89804151&rev_0018#3&1b1819f6&0&03018089fb63494db728d8418b3cbbf549997891#{5
                       3f56307-b6bf-11d0-94f2-00a0c91efb8b}
DriveLetter          : S
Guid                 : {cf468ffa-ae17-4139-a575-717547d4df09}
IsActive             : False
IsBoot               : False
IsHidden             : False
IsOffline            : False
IsReadOnly           : False
IsShadowCopy         : False
IsDAX                : True                   # <- True: DAX enabled
IsSystem             : False
NoDefaultDriveLetter : False
Offset               : 16777216
OperationalStatus    : Online
PartitionNumber      : 2
Size                 : 251.98 GB
Type                 : Basic
```

## <a name="monitoring-health"></a>Мониторинг работоспособности

При использовании постоянной памяти существует несколько отличий в работе мониторинга.

- Постоянная память не создает счетчики производительности физических дисков, поэтому она не отображается на диаграммах в центре администрирования Windows.
- Постоянная память не создает данные Storport 505, поэтому вы не будете получать упреждающее обнаружение выбросов.

Помимо этого, для мониторинга используется тот же процесс, что и для любого другого физического диска. Вы можете запросить работоспособность диска энергонезависимой памяти, выполнив следующие командлеты:

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Unhealthy    None          True         {20, 120}         2
3          252 GB Healthy      None          True         {1020, 1120}      0

Get-PmemDisk | Get-PhysicalDisk | select SerialNumber, HealthStatus, OperationalStatus, OperationalDetails

SerialNumber               HealthStatus OperationalStatus  OperationalDetails
------------               ------------ ------------------ ------------------
802c-01-1602-117cb5fc      Healthy      OK
802c-01-1602-117cb64f      Warning      Predictive Failure {Threshold Exceeded,NVDIMM_N Error}
```

**Хеалсстатус** показывает, исправен ли диск PMem.

Значение **унсафешутдовнкаунт** отслеживает количество завершений работы, которые могут привести к потере данных на этом логическом диске. Это сумма счетчика ненадежного завершения работы всех базовых устройств PMem этого диска. Чтобы получить дополнительные сведения о состоянии работоспособности, используйте командлет **Get-пмемфисикалдевице** , чтобы найти такие сведения, как **OperationalStatus**.

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Unhealthy    {HardwareError}   CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

Этот командлет показывает, какое устройство энергонезависимой памяти неработоспособно. Неработоспособное устройство (**DeviceID** 20) соответствует регистру в предыдущем примере. **Фисикаллокатион** в BIOS может помочь определить, какое устройство энергонезависимой памяти находится в состоянии сбоя.

## <a name="replacing-persistent-memory"></a>Замена энергонезависимой памяти

В этой статье описывается, как просмотреть состояние работоспособности энергонезависимой памяти. Если необходимо заменить неисправный модуль, необходимо повторно выполнить инициализацию диска PMem (см. действия, описанные выше).

При устранении неполадок может потребоваться использовать **Remove-пмемдиск**. Этот командлет удаляет конкретный диск энергонезависимой памяти. Мы можем удалить все текущие диски PMem, выполнив следующие командлеты:

```PowerShell
Get-PmemDisk | Remove-PmemDisk

cmdlet Remove-PmemDisk at command pipeline position 1
Supply values for the following parameters:
DiskNumber: 2

This will remove the persistent memory disk(s) from the system and will result in data loss.
Remove the persistent memory disk(s)?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
Removing the persistent memory disk. This may take a few moments.
```

> [!IMPORTANT]
> Удаление постоянного диска памяти приводит к утере данных на этом диске.

Другой командлет, возможно, потребуется **инициализировать-пмемфисикалдевице**. Этот командлет инициализирует области хранения меток на физических устройствах энергонезависимой памяти и может очистить поврежденные сведения о хранилище меток на устройствах PMem.

```PowerShell
Get-PmemPhysicalDevice | Initialize-PmemPhysicalDevice

This will initialize the label storage area on the physical persistent memory device(s) and will result in data loss.
Initializes the physical persistent memory device(s)?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): A
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
```

> [!IMPORTANT]
> **Initialize-пмемфисикалдевице** вызывает потери данных в энергонезависимой памяти. Используйте его в качестве последнего средства для исправления постоянных проблем, связанных с памятью.

## <a name="additional-references"></a>Дополнительные ссылки

- [Обзор Локальные дисковые пространства](storage-spaces-direct-overview.md)
- [Управление работоспособностью памяти хранилища (NVDIMM-N) в Windows](storage-class-memory-health.md)
- [Общие сведения о кэше](understand-the-cache.md)
