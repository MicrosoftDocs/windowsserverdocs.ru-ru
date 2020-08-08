---
title: Качество обслуживания хранилища
manager: dongill
ms.author: JGerend
ms.topic: get-started-article
ms.assetid: 8dcb8cf9-0e08-4fdd-9d7e-ec577ce8d8a0
author: kumudd
ms.date: 10/10/2016
ms.openlocfilehash: ced2fe051f0595e8333aa2704889cc88ec1304ac
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87994731"
---
# <a name="storage-quality-of-service"></a>Качество обслуживания хранилища

> Применяется к: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)

Представленный в Windows Server 2016 компонент качества обслуживания хранилища позволяет централизованно отслеживать и контролировать производительность хранилища виртуальных машин с помощью ролей Hyper-V и масштабируемого файлового сервера. Этот компонент автоматически обеспечивает равномерное использование ресурсов хранилища между несколькими виртуальными машинами, применяющими один кластер файловых серверов, и позволяет настроить минимальный и максимальный показатели производительности в рамках политики с помощью единиц нормализованных операций ввода-вывода в секунду.

Компонент качества обслуживания хранилища в Windows Server 2016 поддерживает следующие задачи:

-   **Решение проблем, связанных с потреблением ресурсов другими экземплярами.** По умолчанию служба качества обслуживания хранилища гарантирует, что одна виртуальная машина не может использовать все ресурсы хранилища и влиять на пропускную способность для других виртуальных машин.

-   **Комплексный мониторинг производительности хранилища.** Отслеживание производительности виртуальных машин, хранящихся на масштабируемом файловом сервере, начинается сразу после их запуска. Сведения о производительности всех работающих виртуальных машин и конфигурации кластера масштабируемых файловых серверов можно просмотреть из одного расположения.

-   **Управление требованиями к числу операций ввода-вывода в рамках рабочей нагрузки.** Политики службы качества обслуживания хранилища определяют минимальный и максимальный показатели производительности виртуальных машин и гарантируют, что они выполняются. Это обеспечивает согласованную производительность виртуальных машин, даже в загруженных и избыточно подготовленных средах. Если значения, заданные в политиках, не могут быть удовлетворены, активируются оповещения, уведомляющие, что виртуальные машины не соответствуют политике или что им назначены недопустимые политики.

Здесь описываются преимущества нового компонента качества обслуживания хранилища для бизнес-процессов организации. Предполагается, что вы уже знакомы с Windows Server, отказоустойчивой кластеризацией Windows Server, масштабируемым файловым сервером, Hyper-V и Windows PowerShell.

## <a name="overview"></a><a name="BKMK_Overview"></a>Источники данных в Azure Monitor
В этом разделе рассматриваются требования к использованию службы качества обслуживания хранилища, а также приведены общие сведения о программно-определяемом решении, использующем эту службу, и перечень связанных с ней терминов.

### <a name="storage-qos-requirements"></a><a name="BKMK_Requirements"></a>Требования к службе качества обслуживания хранилища
Служба качества обслуживания хранилища поддерживает два сценария развертывания.

-   **Hyper-V с использованием масштабируемого файлового сервера.** Этот сценарий предусматривает наличие следующих компонентов:

    -   Кластер хранилища, представленный кластером масштабируемого файлового сервера.

    -   Вычислительный кластер как минимум с одним сервером и включенной ролью Hyper-V.

    Для службы качества обслуживания хранилища требуется, чтобы на серверах хранилища был отказоустойчивый кластер, но в нем не должны быть вычислительные серверы. Все серверы (и для хранения, и для вычислений) должны работать под управлением Windows Server 2016.

    Если у вас не развернут кластер масштабируемых файловых серверов в целях оценки, пошаговые инструкции по его созданию с использованием имеющихся серверов или виртуальных машин см. в статье [Windows Server 2012 R2 Storage: Step-by-step with Storage Spaces, SMB Scale-Out and Shared VHDX (Physical)](/archive/blogs/josebda/windows-server-2012-r2-storage-step-by-step-with-storage-spaces-smb-scale-out-and-shared-vhdx-physical) (Хранилище Windows Server 2012 R2: пошаговое руководство, включающее использование дисковых пространств, масштабирования SMB и общего диска VHDX (физического)).

-   **Hyper-V с использованием общих томов кластера.** Этот сценарий предусматривает наличие следующих компонентов:

    -   Вычислительный кластер с включенной ролью Hyper-V.

    -   Hyper-V с использованием общих томов кластера для хранения.

Также требуется наличие отказоустойчивого кластера. На всех серверах должна быть установлена одинаковая версия Windows Server 2016.

### <a name="using-storage-qos-in-a-software-defined-storage-solution"></a><a name="BKMK_SolutionOverview"></a>Использование службы качества обслуживания хранилища в программно-определяемом решении для хранения данных
Служба качества обслуживания хранилища встроена в программно-определяемом решении Майкрософт для хранения данных, предоставляемом масштабируемым файловым сервером и Hyper-V. Серверы Hyper-V могут получить доступ к файловым ресурсам на масштабируемом файловом сервере по протоколу SMB3. В кластер файловых серверов добавлен новый диспетчер политик, который обеспечивает централизованный мониторинг производительности хранилища.

![Масштабируемый файловый сервер и качество обслуживания хранилища](media/overview-Clustering_SOFSStorageQoS.png)

**Рис. 1. Использование службы качества обслуживания хранилища в программно-определяемом решении для хранения данных на масштабируемом файловом сервере**

Так как серверы Hyper-V запускают виртуальные машины, они отслеживаются с помощью диспетчера политик. Диспетчер политик сообщает политику качества обслуживания хранилища и ограничения или резервирования серверу Hyper-V, который соответствующим образом управляет производительностью виртуальной машины.

При изменении политик качества обслуживания хранилища или требований к производительности виртуальных машин диспетчер политик уведомляет серверы Hyper-V, что нужно отрегулировать поведение. Такая цепь обратной связи гарантирует, что все виртуальные жесткие диски виртуальных машин работают согласованно в соответствии с политиками качества обслуживания хранилища.

### <a name="glossary"></a><a name="BKMK_Glossary"></a>Глоссарий

|Термин|Описание|
|--------|---------------|
|Нормализованные операции ввода-вывода в секунду|В этих единицах измеряется использование хранилища.  Это число операций ввода-вывода хранилища в секунду.  Операция ввода-вывода размером 8 КБ или меньше считается одной нормализованной операцией ввода-вывода.  Если размер такой операции превышает 8 КБ, она рассматривается как несколько нормализованных операций ввода-вывода. Например, запрос размером 256 КБ рассматривается как 32 нормализованные операции ввода-вывода в секунду.<p>В Windows Server 2016 можно указать размер для нормализации операций ввода-вывода.  В кластере хранилища можно указать нормализованный размер, который будет применяться при вычислении нормализации на уровне всего кластера.  Значение по умолчанию — 8 КБ.|
|Поток|Это каждый дескриптор файла, который открывает сервер Hyper-V для файла VHD или VHDX (так называемый "поток"). Если к виртуальной машине присоединены два виртуальных жестких диска, на каждый файл вызывается 1 поток для кластера файловых серверов. Если VHDX совместно используется несколькими виртуальными машинами, на каждую виртуальную машину вызывается 1 поток.|
|InitiatorName (Имя инициатора)|Имя виртуальной машины, сообщаемое масштабируемому файловому серверу для каждого потока.|
|InitiatorID (Идентификатор инициатора)|Идентификатор, соответствующий ИД виртуальной машины.  Его всегда можно использовать, чтобы однозначно идентифицировать виртуальные машины с отдельными потоками, даже если эти машины имеют одинаковое имя инициатора.|
|Политика|Политики службы качества обслуживания хранилища хранятся в базе данных кластера и имеют следующие свойства: PolicyId, MinimumIOPS, MaximumIOPS, ParentPolicy и PolicyType.|
|PolicyId|Уникальный идентификатор политики.  Он формируется по умолчанию, но при необходимости его можно задать самостоятельно.|
|MinimumIOPS (Минимальное значение IOPS)|Минимальное число нормализованных операций ввода-вывода в секунду, определенных в политике.  Также называется резервированием.|
|MaximumIOPS (Максимальное значение IOPS)|Максимальное число нормализованных операций ввода-вывода в секунду, определенных в политике.  Также называется ограничением.|
|Aggregated (Объединенная) |Тип политики, при которой указанные минимальное и максимальное значения IOPS, а также значение пропускной способности являются общими для всех потоков, которым назначена политика. Всем VHD, для которых назначена политика в системе хранения, выделена общая пропускная способность ввода-вывода.|
|Выделенные|Тип политики, при которой указанные минимальное и максимальное значения IOPS, а также значение пропускной способности используются для одного VHD или VHDX.|

## <a name="how-to-set-up-storage-qos-and-monitor-basic-performance"></a><a name="BKMK_SetUpQoS"></a>Как настроить службу качества обслуживания хранилища и выполнять мониторинг базовых показателей производительности
В этом разделе показано, как включить новый компонент качества обслуживания хранилища и отслеживать производительность хранилища без применения пользовательских политик.

### <a name="set-up-storage-qos-on-a-storage-cluster"></a><a name="BKMK_SetupStorageQoSonStorageCluster"></a>Настройка компонента качества обслуживания хранилища в кластере хранилища
В этом разделе вы узнаете, как настроить службу качества обслуживания хранилища в новом или имеющемся отказоустойчивом кластере и масштабируемом файловом сервере, на котором работает Windows Server 2016.

#### <a name="set-up-storage-qos-on-a-new-installation"></a>Настройка компонента качества обслуживания хранилища в новой системе
Если в Windows Server 2016 настроен новый отказоустойчивый кластер и общий том кластера (CSV), компонент качества обслуживания хранилища будет настроен автоматически.

#### <a name="verify-storage-qos-installation"></a>Проверка установки компонента качества обслуживания хранилища
После создания отказоустойчивого кластера и настройки диска CSV **компонент качества обслуживания хранилища** распознается как основной ресурс кластера и отображается в Windows PowerShell и диспетчере отказоустойчивости кластеров. Таким образом, система отказоустойчивого кластера будет управлять этим ресурсом без вашего вмешательства.  Этот ресурс отображается и в диспетчере отказоустойчивости кластеров, и в PowerShell для согласованности с другими ресурсами системы отказоустойчивого кластера, такими как новая служба работоспособности.

![Ресурс качества обслуживания хранилища отображается в окне "Ресурсы ядра кластера"](media/overview-Clustering_StorageQoSFCM.png)

**Рис. 2. Ресурс качества обслуживания хранилища, отображаемый как основной ресурс кластера в диспетчере отказоустойчивости кластеров**

Чтобы просмотреть состояние ресурса качества обслуживания хранилища, воспользуйтесь следующим командлетом PowerShell:

```PowerShell
PS C:\> Get-ClusterResource -Name "Storage Qos Resource"

Name                   State      OwnerGroup        ResourceType
----                   -----      ----------        ------------
Storage Qos Resource   Online     Cluster Group     Storage QoS Policy Manager
```

### <a name="set-up-storage-qos-on-a-compute-cluster"></a><a name="BKMK_SetupStorageQoSonComputeCluster"></a>Настройка компонента качества обслуживания хранилища в вычислительном кластере
Роль Hyper-V в Windows Server 2016 имеет встроенную поддержку службы качества обслуживания хранилища, которая включена по умолчанию.

#### <a name="install-remote-administration-tools-to-manage-storage-qos-policies-from-remote-computers"></a>Установка средств удаленного администрирования для управления политиками качества обслуживания хранилища с удаленных компьютеров
С помощью средств удаленного администрирования сервера можно управлять политиками качества обслуживания хранилища и отслеживать потоки из вычислительных узлов.  Эти средства доступны в качестве дополнительных компонентов во всех пакетах установки Windows Server 2016. Их также можно скачать отдельно для Windows 10 на веб-сайте [Центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=45520).

Дополнительный компонент **RSAT-Clustering** включает в себя модуль Windows PowerShell для удаленного управления отказоустойчивым кластером, а также компонент качества обслуживания хранилища.

-   Windows PowerShell: Add-WindowsFeature RSAT-Clustering.

Дополнительный компонент **RSAT-Hyper-V-Tools** включает в себя модуль Windows PowerShell для удаленного управления Hyper-V.

-   Windows PowerShell: Add-WindowsFeature RSAT-Hyper-V-Tools.

#### <a name="deploy-virtual-machines-to-run-workloads-for-testing"></a>Развертывание виртуальных машин для запуска тестовых рабочих нагрузок
На масштабируемом файловом сервере потребуется развернуть несколько виртуальных машин с соответствующими рабочими нагрузками.  Советы по моделированию нагрузки и нагрузочному тестированию см. в записи блога [DiskSpd, PowerShell и производительность хранилища: измерение числа операций ввода-вывода в секунду, пропускной способности и задержки для локальных дисков и общих папок SMB](/archive/blogs/josebda/diskspd-powershell-and-storage-performance-measuring-iops-throughput-and-latency-for-both-local-disks-and-smb-file-shares), где описано рекомендуемое средство (DiskSpd) и приведены некоторые примеры использования.

В примерах сценариев, приведенных в данном руководстве, используется пять виртуальных машин. На виртуальных машинах BuildVM1, BuildVM2, BuildVM3 и BuildVM4 выполняется рабочая нагрузка рабочего стола с низкими и средними требованиями к хранилищу. На виртуальной машине TestVm1 выполняется тест производительности оперативной обработки транзакций с высокими требованиями к хранилищу.

### <a name="view-current-storage-performance-metrics"></a>Просмотр текущих метрик производительности хранилища
Этот раздел состоит из следующих частей.

-   запрос потоков с помощью командлета `Get-StorageQosFlow`;

-   просмотр данных производительности тома с помощью командлета `Get-StorageQosVolume`.

#### <a name="query-flows-using-the-get-storageqosflow-cmdlet"></a>Запрос потоков с помощью командлета Get-StorageQosFlow

Командлет Get-StorageQosFlow показывает все текущие потоки, инициированные серверами Hyper-V. Кластер масштабируемых файловых серверов собирает все данные, поэтому командлет можно использовать на любом узле в этом кластере или на удаленном сервере с указанием параметра -CimSession.

**Команда в следующем примере показывает, как просмотреть все файлы, открытые с помощью Hyper-V на сервере, с использованием командлета Get-StorageQoSFlow**.

```PowerShell
PS C:\> Get-StorageQosFlow

InitiatorName    InitiatorNodeNam StorageNodeName  FilePath        Status
                 e
-------------    ---------------- ---------------  --------        ------
                                  plang-fs3.pla... C:\ClusterSt... Ok
                                  plang-fs2.pla... C:\ClusterSt... Ok
                                  plang-fs1.pla... C:\ClusterSt... Ok
                                  plang-fs3.pla... C:\ClusterSt... Ok
                                  plang-fs2.pla... C:\ClusterSt... Ok
                                  plang-fs1.pla... C:\ClusterSt... Ok
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok
BuildVM4         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok
WinOltp1         plang-c1.plan... plang-fs1.pla... C:\ClusterSt... Ok
BuildVM3         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok
BuildVM1         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok
BuildVM2         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok
                                  plang-fs3.pla... C:\ClusterSt... Ok
                                  plang-fs2.pla... C:\ClusterSt... Ok
BuildVM4         plang-c2.plan... plang-fs2.pla... C:\ClusterSt... Ok
WinOltp1         plang-c1.plan... plang-fs2.pla... C:\ClusterSt... Ok
BuildVM3         plang-c2.plan... plang-fs2.pla... C:\ClusterSt... Ok
WinOltp1         plang-c1.plan... plang-fs2.pla... C:\ClusterSt... Ok
                                  plang-fs1.pla... C:\ClusterSt... Ok
```

Команда в следующем примере отформатирована и отображает имена виртуальной машины, узла Hyper-V и VHD-файла, отсортированные по числу операций ввода-вывода в секунду.

```PowerShell
PS C:\> Get-StorageQosFlow | Sort-Object StorageNodeIOPs -Descending | ft InitiatorName, @{Expression={$_.InitiatorNodeName.Substring(0,$_.InitiatorNodeName.IndexOf('.'))};Label="InitiatorNodeName"}, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName InitiatorNodeName StorageNodeIOPs Status File
------------- ----------------- --------------- ------ ----
WinOltp1      plang-c1                     3482     Ok IOMETER.VHDX
BuildVM2      plang-c2                      544     Ok BUILDVM2.VHDX
BuildVM1      plang-c2                      497     Ok BUILDVM1.VHDX
BuildVM4      plang-c2                      316     Ok BUILDVM4.VHDX
BuildVM3      plang-c2                      296     Ok BUILDVM3.VHDX
BuildVM4      plang-c2                      195     Ok WIN8RTM_ENTERPRISE_VL_BU...
TR20-VMM      plang-z400                    156     Ok DATA1.VHDX
BuildVM3      plang-c2                       81     Ok WIN8RTM_ENTERPRISE_VL_BU...
WinOltp1      plang-c1                       65     Ok BOOT.VHDX
                                             18     Ok DefaultFlow
                                             12     Ok DefaultFlow
WinOltp1      plang-c1                        4     Ok 9914.0.AMD64FRE.WINMAIN....
TR20-VMM      plang-z400                      4     Ok DATA2.VHDX
TR20-VMM      plang-z400                      3     Ok BOOT.VHDX
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
                                              0     Ok DefaultFlow
```

Команда в следующем примере показывает, как отфильтровать потоки по InitiatorName, чтобы с легкостью найти данные производительности хранилища и параметры для конкретной виртуальной машины.

```PowerShell
PS C:\> Get-StorageQosFlow -InitiatorName BuildVm1 | Format-List

FilePath           : C:\ClusterStorage\Volume2\SHARES\TWO\BUILDWORKLOAD\BUILDVM1.V
                     HDX
FlowId             : ebfecb54-e47a-5a2d-8ec0-0940994ff21c
InitiatorId        : ae4e3dd0-3bde-42ef-b035-9064309e6fec
InitiatorIOPS      : 464
InitiatorLatency   : 26.2684
InitiatorName      : BuildVM1
InitiatorNodeName  : plang-c2.plang.nttest.microsoft.com
Interval           : 300000
Limit              : 500
PolicyId           : b145e63a-3c9e-48a8-87f8-1dfc2abfe5f4
Reservation        : 500
Status             : Ok
StorageNodeIOPS    : 475
StorageNodeLatency : 7.9725
StorageNodeName    : plang-fs1.plang.nttest.microsoft.com
TimeStamp          : 2/12/2015 2:58:49 PM
VolumeId           : 4d91fc3a-1a1e-4917-86f6-54853b2a6787
PSComputerName     :
MaximumIops        : 500
MinimumIops        : 500
```

Командлет `Get-StorageQosFlow` возвращает следующие данные:

-   Имя узла Hyper-V (InitiatorNodeName).

-   Имя виртуальной машины и ее идентификатор (InitiatorName и InitiatorId).

-   Последние средние данные производительности, наблюдаемые узлом Hyper-V для виртуального диска (InitiatorIOPS, InitiatorLatency).

-   Последние средние данные производительности, наблюдаемые кластером хранилища для виртуального диска (StorageNodeIOPS, StorageNodeLatency).

-   Текущая политика, применяемая к файлу (при наличии), и итоговая конфигурация (PolicyId, Reservation, Limit).

-   Состояние политики:

    -   **Ok** — проблемы отсутствуют.

    -   InsufficientThroughput — политика применяется, но минимальное значение IOPS не может быть достигнуто.  Это может происходить, если минимальное значение для виртуальной машины или всех виртуальных машин не соответствует размеру тома хранилища.

    -   **UnknownPolicyId** — политика назначена виртуальной машине на узле Hyper-V, но отсутствует на файловом сервере.  Следует удалить эту политику из конфигурации виртуальной машины или создать такую же политику в кластере файловых серверов.

#### <a name="view-performance-for-a-volume-using-get-storageqosvolume"></a>Просмотр данных производительности тома с помощью командлета Get-StorageQosVolume
Метрики производительности хранилища также собираются на уровне тома каждого хранилища в дополнение к метрикам производительности для каждого потока.  Из этих сведений можно узнать среднее общее использование нормализованных операций ввода-вывода в секунду, задержку, совокупные ограничения и резервирования, применяемые к тому.

```PowerShell
PS C:\> Get-StorageQosVolume | Format-List

Interval       : 300000
IOPS           : 0
Latency        : 0
Limit          : 0
Reservation    : 0
Status         : Ok
TimeStamp      : 2/12/2015 2:59:38 PM
VolumeId       : 434f561f-88ae-46c0-a152-8c6641561504
PSComputerName :
MaximumIops    : 0
MinimumIops    : 0

Interval       : 300000
IOPS           : 1097
Latency        : 3.1524
Limit          : 0
Reservation    : 1568
Status         : Ok
TimeStamp      : 2/12/2015 2:59:38 PM
VolumeId       : 4d91fc3a-1a1e-4917-86f6-54853b2a6787
PSComputerName :
MaximumIops    : 0
MinimumIops    : 1568

Interval       : 300000
IOPS           : 5354
Latency        : 6.5084
Limit          : 0
Reservation    : 781
Status         : Ok
TimeStamp      : 2/12/2015 2:59:38 PM
VolumeId       : 0d2fd367-8d74-4146-9934-306726913dda
PSComputerName :
MaximumIops    : 0
MinimumIops    : 781
```

## <a name="how-to-create-and-monitor-storage-qos-policies"></a><a name="BKMK_CreateQoSPolicies"></a>Как создать и отслеживать политики качества обслуживания хранилища
В этом разделе описано, как создать политики качества обслуживания хранилища, применить их к виртуальным машинам и отслеживать кластер хранилища после их применения.

### <a name="create-storage-qos-policies"></a>Создание политик качества обслуживания хранилища
Определение политик качества обслуживания хранилища и управление ими осуществляется в кластере масштабируемых файловых серверов.  Вы можете создать любое необходимое количество политик для развертывания (до 10 000 на кластер хранилища).

Для каждого VHD- или VHDX-файла, назначенного виртуальной машине, можно настроить политику. Разные файлы и виртуальные машины могут использовать как одну общую, так и отдельные политики.  Если для нескольких VHD- или VHDX-файлов либо нескольких виртуальных машин настроена одна политика, они будут рассматриваться вместе и между ними будет одинаково разделено минимальное и максимальное значения IOPS. Если вы используете отдельные политики для нескольких виртуальных машин либо VHD- или VHDX-файлов, минимальное и максимальное значения будут отслеживаться для них отдельно.

Если создать несколько одинаковых политик для разных виртуальных машин с аналогичными требованиями к хранилищу, они получат одинаковое число операций ввода-вывода в секунду.  Если требования к хранилищу у виртуальных машин разные, число операций ввода-вывода в секунду будет распределяться в соответствии с требованиями.

### <a name="types-of-storage-qos-policies"></a>Типы политик качества обслуживания хранилища
Есть два типа политик: объединенная, или Aggregated (ранее называвшаяся SingleInstance, или одноэкземплярной), и выделенная, или Dedicated (ранее называвшаяся MultiInstance, или многоэкземплярной). Объединенные политики применяют максимальные и минимальные значения для объединенного набора VHD- или VHDX-файлов и виртуальных машин, которым они назначены. Таким образом, у них общий набор операций ввода-вывода в секунду и пропускная способность. Выделенные политики применяют максимальные и минимальные значения для каждого VHD- или VHDX-файла отдельно. Поэтому можно создать одну политику, которая применяет одинаковые ограничения к нескольким VHD- или VHDX-файлам.

Например, если создать объединенную политику, где минимальное число операций ввода-вывода в секунду — 300, а максимальное — 500, и применить эту политику к 5 разным VHD- или VHDX-файлам, у всех этих файлов вместе гарантировано будет минимум 300 (если есть соответствующий спрос и система хранения может предоставить такую производительность) и максимум 500 IOPS. Если у всех этих файлов одинаковые требования к операциям ввода-вывода в секунду и достаточно ресурсов хранения, каждый из этих файлов получит примерно по 100 таких операций.

Однако если создать выделенную политику с аналогичными ограничениями и применить ее к VHD- или VHDX-файлам на 5 разных виртуальных машинах, каждая виртуальная машина получит не менее 300 и не более 500 операций ввода-вывода в секунду. Если у виртуальных машин одинаковые требования к операциям ввода-вывода в секунду и достаточно ресурсов хранения, каждая из них получит примерно по 500 таких операций. .  Если у одной из виртуальных машин несколько VHD- или VHDX-файлов с одинаковой многоэкземплярной политикой, к ним будет применяться общее ограничение. Таким образом, общее число операций ввода-вывода в секунду для виртуальной машины из файлов с этой политикой не может превышать ограничение.

Поэтому, если у вас есть несколько VHD- или VHDX-файлов, у которых должна быть одинаковая производительность, и вы не хотите создавать несколько одинаковых политик, можно использовать одну выделенную политику, которая будет применяться к файлам каждой виртуальной машины.

Не более 20 файлов VHD и VHDx, назначенных одной совокупной политике.  Этот тип политики предназначен для объединения с небольшими виртуальными машинами в кластере.

### <a name="create-and-apply-a-dedicated-policy"></a>Создание и применение выделенной политики
Сначала используйте командлет `New-StorageQosPolicy`, чтобы создать политику на масштабируемом файловом сервере, как показано в следующем примере.

```PowerShell
$desktopVmPolicy = New-StorageQosPolicy -Name Desktop -PolicyType Dedicated -MinimumIops 100 -MaximumIops 200
```

Затем примените ее к соответствующим жестким дискам виртуальных машин на сервере Hyper-V.  Запишите значение PolicyId из предыдущего шага или сохраните его в переменной в скриптах.

Используя PowerShell, на масштабируемом файловом сервере создайте политику качества обслуживания хранилища и получите ее идентификатор, как показано в следующем примере.

```PowerShell
PS C:\> $desktopVmPolicy = New-StorageQosPolicy -Name Desktop -PolicyType Dedicated -MinimumIops 100 -MaximumIops 200

C:\> $desktopVmPolicy.PolicyId

Guid
----
cd6e6b87-fb13-492b-9103-41c6f631f8e0
```

Используя PowerShell, на сервере Hyper-V настройте политику качества обслуживания хранилища с использованием идентификатора, как показано в следующем примере.

```PowerShell
Get-VM -Name Build* | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID cd6e6b87-fb13-492b-9103-41c6f631f8e0
```

### <a name="confirm-that-the-policies-are-applied"></a>Проверка того, применяются ли политики
Используйте командлет PowerShell `Get-StorageQosFlow`, чтобы проверить, применяются ли минимальное и максимальное значения IOPS к соответствующим потокам, как показано в следующем примере.

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName |
 ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName Status MinimumIops MaximumIops StorageNodeIOPs Status File
------------- ------ ----------- ----------- --------------- ------ ----
BuildVM1          Ok         100         200             250     Ok BUILDVM1.VHDX
BuildVM2          Ok         100         200             251     Ok BUILDVM2.VHDX
BuildVM3          Ok         100         200             252     Ok BUILDVM3.VHDX
BuildVM4          Ok         100         200             233     Ok BUILDVM4.VHDX
TR20-VMM          Ok          33         666               1     Ok DATA2.VHDX
TR20-VMM          Ok          33         666               5     Ok DATA1.VHDX
TR20-VMM          Ok          33         666               4     Ok BOOT.VHDX
WinOltp1          Ok           0           0               0     Ok 9914.0.AMD6...
WinOltp1          Ok           0           0            5166     Ok IOMETER.VHDX
WinOltp1          Ok           0           0               0     Ok BOOT.VHDX
```

На сервере Hyper-V можно также использовать скрипт **Get-VMHardDiskDrivePolicy.ps1**, чтобы узнать, какая политика применяется к виртуальному жесткому диску.

```PowerShell
PS C:\> Get-VM -Name BuildVM1 | Get-VMHardDiskDrive | Format-List

Path                          : \\plang-fs.plang.nttest.microsoft.com\two\BuildWorkload
                                \BuildVM1.vhdx
DiskNumber                    :
MaximumIOPS                   : 0
MinimumIOPS                   : 0
QoSPolicyID                   : cd6e6b87-fb13-492b-9103-41c6f631f8e0
SupportPersistentReservations : False
ControllerLocation            : 0
ControllerNumber              : 0
ControllerType                : IDE
PoolName                      : Primordial
Name                          : Hard Drive
Id                            : Microsoft:AE4E3DD0-3BDE-42EF-B035-9064309E6FEC\83F8638B
                                -8DCA-4152-9EDA-2CA8B33039B4\0\0\D
VMId                          : ae4e3dd0-3bde-42ef-b035-9064309e6fec
VMName                        : BuildVM1
VMSnapshotId                  : 00000000-0000-0000-0000-000000000000
VMSnapshotName                :
ComputerName                  : PLANG-C2
IsDeleted                     : False
```

### <a name="query-for-storage-qos-policies"></a>Запрос политик качества обслуживания хранилища
`Get-StorageQosPolicy`Список всех настроенных политик и их состояние на масштабируемый файловый сервер.

```PowerShell
PS C:\> Get-StorageQosPolicy

Name                 MinimumIops          MaximumIops          Status
----                 -----------          -----------          ------
Default              0                    0                    Ok
Limit500             0                    500                  Ok
SilverVm             500                  500                  Ok
Desktop              100                  200                  Ok
Limit500             0                    0                    Ok
VMM                  100                  2000                 Ok
Vdi                  1                    100                  Ok
```

Со временем состояние может изменяться в зависимости от работы системы.

-   **Ok** — все потоки, для которых применяется эта политика, получают запрошенное минимальное количество IOPS.

-   **InsufficientThroughput** — один или несколько потоков, для которых применяется эта политика, не получают минимальное количество IOPS.

Можно также передать политику в командлет `Get-StorageQosPolicy`, чтобы получить состояние всех потоков, настроенных для использования политики.

```PowerShell
PS C:\> Get-StorageQosPolicy -Name Desktop | Get-StorageQosFlow | ft InitiatorName, *IOPS, Status, FilePath -AutoSize

InitiatorName MaximumIops MinimumIops InitiatorIOPS StorageNodeIOPS Status FilePat
                                                                           h
------------- ----------- ----------- ------------- --------------- ------ -------
BuildVM4              100          50           187              17     Ok C:\C...
BuildVM3              100          50           194              25     Ok C:\C...
BuildVM1              200         100           195             196     Ok C:\C...
BuildVM2              200         100           193             192     Ok C:\C...
BuildVM4              200         100           187             169     Ok C:\C...
BuildVM3              200         100           194             169     Ok C:\C...
```

### <a name="create-an-aggregated-policy"></a>Создание объединенной политики
Объединенные политики можно использовать, если требуется, чтобы несколько виртуальных жестких дисков использовали один пул операций ввода-вывода и объем пропускной способности.  Например, если применить ту же объединенную политику к жестким дискам двух виртуальных машин, минимальное количество будет разделено между ними в соответствии с требованиями.  Оба диска гарантированно получат объединенное минимальное значение и вместе не превысят заданное максимальное значение IOPS или пропускной способности.

Тот же подход можно использовать для общего выделения ресурсов для всех VHD- или VHDX-файлов для виртуальных машин, составляющих службу или принадлежащих клиенту в многоузловой среде.

Процедура создания обеих политик (выделенной и объединенной) отличается лишь тем, что задаются разные типы политики.

В следующем примере показано, как на масштабируемом файловом сервере создать объединенную политику для качества обслуживания хранилища и получить ее идентификатор.

```PowerShell
PS C:\> $highPerf = New-StorageQosPolicy -Name SqlWorkload -MinimumIops 1000 -MaximumIops 5000 -PolicyType Aggregated
[plang-fs]: PS C:\Users\plang\Documents> $highPerf.PolicyId

Guid
----
7e2f3e73-1ae4-4710-8219-0769a4aba072
```

В следующем примере показано, как применить политику качества обслуживания хранилища на сервере Hyper-V с использованием идентификатора, полученного в предыдущем примере.

```PowerShell
PS C:\> Get-VM -Name WinOltp1 | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID 7e2f3e73-1ae4-4710-8219-0769a4aba072
```

В следующем примере показано, как просмотреть последствия применения политики для качества обслуживания хранилища на файловом сервере.

```PowerShell
PS C:\> Get-StorageQosFlow -InitiatorName WinOltp1 | format-list InitiatorName, PolicyId, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, FilePath

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 250
MaximumIops     : 1250
StorageNodeIOPs : 0
FilePath        : C:\ClusterStorage\Volume2\SHARES\TWO\BASEVHD\9914.0.AMD64FRE.WIN
                  MAIN.141218-1718_SERVER_SERVERDATACENTER_EN-US.VHDX

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 250
MaximumIops     : 1250
StorageNodeIOPs : 0
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\BOOT.VHDX

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 1000
MaximumIops     : 5000
StorageNodeIOPs : 4550
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX
PS C:\> Get-StorageQosFlow -InitiatorName WinOltp1 | for
mat-list InitiatorName, PolicyId, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, FilePath

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 250
MaximumIops     : 1250
StorageNodeIOPs : 0
FilePath        : C:\ClusterStorage\Volume2\SHARES\TWO\BASEVHD\9914.0.AMD64FRE.WIN
                  MAIN.141218-1718_SERVER_SERVERDATACENTER_EN-US.VHDX

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 250
MaximumIops     : 1250
StorageNodeIOPs : 0
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\BOOT.VHDX

InitiatorName   : WinOltp1
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072
MinimumIops     : 1000
MaximumIops     : 5000
StorageNodeIOPs : 4550
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX
```

Минимальное и максимальное значения IOPS, а также максимальная пропускная способность операций ввода-вывода для каждого виртуального жесткого диска будет регулироваться с учетом загрузки.  Это гарантирует, что общий объем пропускной способности, используемой для группы дисков, будет в пределах диапазона, определенного политикой.  В приведенном выше примере первые два диска неактивны, поэтому третий может использовать максимальное число IOPS.  Если первые два диска снова выполняют операции ввода-вывода, максимальное число IOPS для третьего диска будет автоматически снижено.

### <a name="modify-an-existing-policy"></a>Изменение имеющейся политики
После создания политики можно изменить такие свойства, как имя, минимальное и максимальное значения IOPS, а также максимальная пропускная способность операций ввода-вывода.  Однако изменить тип политики (объединенная или выделенная) нельзя.

В следующем примере показано, как с помощью командлета Windows PowerShell изменить свойство MaximumIOPs для имеющейся политики.

```PowerShell
[DBG]: PS C:\demoscripts>> Get-StorageQosPolicy -Name SqlWorkload | Set-StorageQosPolicy -MaximumIops 6000
```

Следующий командлет проверяет изменения:

```PowerShell
PS C:\> Get-StorageQosPolicy -Name SqlWorkload

Name                    MinimumIops            MaximumIops            Status
----                    -----------            -----------            ------
SqlWorkload             1000                   6000                   Ok

[plang-fs1]: PS C:\Users\plang\Documents> Get-StorageQosPolicy -Name SqlWorkload | Get-Storag
eQosFlow | Format-Table InitiatorName, PolicyId, MaximumIops, MinimumIops, StorageNodeIops -A
utoSize

InitiatorName PolicyId                             MaximumIops MinimumIops StorageNodeIops
------------- --------                             ----------- ----------- ---------------
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        1500         250               0
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        1500         250               0
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        6000        1000            4507
```

## <a name="how-to-identify-and-address-common-issues"></a><a name="BKMK_KnownIssues"></a>Как определить и устранить распространенные проблемы
В этом разделе описано, как найти виртуальные машины с недопустимыми политиками качества обслуживания хранилища, повторно создать соответствующую политику, удалить политику из виртуальной машины и определить виртуальные машины, которые не соответствуют требованиям политики качества обслуживания хранилища.

### <a name="identify-virtual-machines-with-invalid-policies"></a><a name="BKMK_FindingVMsWithInvalidPolicies"></a>Определение виртуальных машин с недопустимыми политиками

Если удалить политику из файлового сервера до ее удаления из виртуальной машины, то виртуальная машина продолжит выполняться, как будто бы политика не была применена.

```PowerShell
PS C:\> Get-StorageQosPolicy -Name SqlWorkload | Remove-StorageQosPolicy

Confirm
Are you sure you want to perform this action?
Performing the operation "DeletePolicy" on target "MSFT_StorageQoSPolicy (PolicyId =
"7e2f3e73-1ae4-4710-8219-0769a4aba072")".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [?] Help (default is "Y"):
```

В этом случае поток будет находиться в состоянии UnknownPolicyId.

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName          Status MinimumIops MaximumIops StorageNodeIOPs          Status File
-------------          ------ ----------- ----------- ---------------          ------ ----
                           Ok           0           0               0              Ok Def...
                           Ok           0           0              10              Ok Def...
                           Ok           0           0              13              Ok Def...
                           Ok           0           0               0              Ok Def...
                           Ok           0           0               0              Ok Def...
                           Ok           0           0               0              Ok Def...
                           Ok           0           0               0              Ok Def...
                           Ok           0           0               0              Ok Def...
                           Ok           0           0               0              Ok Def...
BuildVM1                   Ok         100         200             193              Ok BUI...
BuildVM2                   Ok         100         200             196              Ok BUI...
BuildVM3                   Ok          50          64              17              Ok WIN...
BuildVM3                   Ok          50         136             179              Ok BUI...
BuildVM4                   Ok          50         100              23              Ok WIN...
BuildVM4                   Ok         100         200             173              Ok BUI...
TR20-VMM                   Ok          33         666               2              Ok DAT...
TR20-VMM                   Ok          25         975               3              Ok DAT...
TR20-VMM                   Ok          75        1025              12              Ok BOO...
WinOltp1      UnknownPolicyId           0           0               0 UnknownPolicyId 991...
WinOltp1      UnknownPolicyId           0           0            4926 UnknownPolicyId IOM...
WinOltp1      UnknownPolicyId           0           0               0 UnknownPolicyId BOO...
```

#### <a name="recreate-a-matching-storage-qos-policy"></a><a name="BKMK_RecreateMatchingPolicy"></a>Повторное создание соответствующей политики качества обслуживания хранилища
Если политика была случайно удалена, вы можете создать новую, используя старый идентификатор.  Сначала получите необходимый идентификатор политики.

```PowerShell
PS C:\> Get-StorageQosFlow -Status UnknownPolicyId | ft InitiatorName, PolicyId -AutoSize

InitiatorName PolicyId
------------- --------
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072
```

Затем создайте политику, используя этот идентификатор.

```PowerShell
PS C:\> New-StorageQosPolicy -PolicyId 7e2f3e73-1ae4-4710-8219-0769a4aba072 -PolicyType Aggregated -Name RestoredPolicy -MinimumIops 100 -MaximumIops 2000

Name                    MinimumIops            MaximumIops            Status
----                    -----------            -----------            ------
RestoredPolicy          100                    2000                   Ok
```

Наконец, убедитесь, что она применена.

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName Status MinimumIops MaximumIops StorageNodeIOPs Status File
------------- ------ ----------- ----------- --------------- ------ ----
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               8     Ok DefaultFlow
                  Ok           0           0               9     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
                  Ok           0           0               0     Ok DefaultFlow
BuildVM1          Ok         100         200             192     Ok BUILDVM1.VHDX
BuildVM2          Ok         100         200             193     Ok BUILDVM2.VHDX
BuildVM3          Ok          50         100              24     Ok WIN8RTM_ENTERPRISE_VL...
BuildVM3          Ok         100         200             166     Ok BUILDVM3.VHDX
BuildVM4          Ok          50         100              12     Ok WIN8RTM_ENTERPRISE_VL...
BuildVM4          Ok         100         200             178     Ok BUILDVM4.VHDX
TR20-VMM          Ok          33         666               2     Ok DATA2.VHDX
TR20-VMM          Ok          33         666               2     Ok DATA1.VHDX
TR20-VMM          Ok          33         666              10     Ok BOOT.VHDX
WinOltp1          Ok          25         500               0     Ok 9914.0.AMD64FRE.WINMA...
```

#### <a name="remove-storage-qos-policies"></a><a name="BKMK_RemovePolicyFromVM"></a>Удаление политик качества обслуживания хранилища

Если политика была случайно удалена или если виртуальная машина была импортирована с ненужной политикой, ее можно удалить.

```PowerShell
PS C:\> Get-VM -Name WinOltp1 | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID $null
```

После удаления идентификатора политики из параметров виртуального жесткого диска состояние изменится на Ok. При этом минимальные и максимальные значения применяться не будут.

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName MinimumIops MaximumIops StorageNodeIOPs Status File
------------- ----------- ----------- --------------- ------ ----
                        0           0               0     Ok DefaultFlow
                        0           0              16     Ok DefaultFlow
                        0           0              12     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
                        0           0               0     Ok DefaultFlow
BuildVM1              100         200             197     Ok BUILDVM1.VHDX
BuildVM2              100         200             192     Ok BUILDVM2.VHDX
BuildVM3                9           9              23     Ok WIN8RTM_ENTERPRISE_VL_BUILDW...
BuildVM3               91         191             171     Ok BUILDVM3.VHDX
BuildVM4                8           8              18     Ok WIN8RTM_ENTERPRISE_VL_BUILDW...
BuildVM4               92         192             163     Ok BUILDVM4.VHDX
TR20-VMM               33         666               2     Ok DATA2.VHDX
TR20-VMM               33         666               1     Ok DATA1.VHDX
TR20-VMM               33         666               5     Ok BOOT.VHDX
WinOltp1                0           0               0     Ok 9914.0.AMD64FRE.WINMAIN.1412...
WinOltp1                0           0            1811     Ok IOMETER.VHDX
WinOltp1                0           0               0     Ok BOOT.VHDX
```

### <a name="find-virtual-machines-that-are-not-meeting-storage-qos-policies"></a><a name="BKMK_VMsThatDoNotMeetStorageQoSPoilicies"></a>Поиск виртуальных машин, несоответствующих требованиям политик качества обслуживания хранилища
Состояние **InsufficientThroughput** назначается всем потокам, которые соответствуют следующим требованиям:

-   в назначенной им политике задано минимальное число операций ввода-вывода в секунду;

-   они инициируют операции ввода-вывода при достижении или превышении минимального значения;

-   они не достигают минимального значения операций ввода-вывода.

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize

InitiatorName MinimumIops MaximumIops StorageNodeIOPs                 Status File
------------- ----------- ----------- ---------------                 ------ ----
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0              15                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
                        0           0               0                     Ok DefaultFlow
BuildVM3               50         100              20                     Ok WIN8RTM_ENTE...
BuildVM3              100         200             174                     Ok BUILDVM3.VHDX
BuildVM4               50         100              11                     Ok WIN8RTM_ENTE...
BuildVM4              100         200             188                     Ok BUILDVM4.VHDX
TR20-VMM               33         666               3                     Ok DATA1.VHDX
TR20-VMM               78        1032             180                     Ok BOOT.VHDX
TR20-VMM               22         968               4                     Ok DATA2.VHDX
WinOltp1             3750        5000               0                     Ok 9914.0.AMD64...
WinOltp1            15000       20000           11679 InsufficientThroughput IOMETER.VHDX
WinOltp1             3750        5000               0                     Ok BOOT.VHDX
```

Потоки можно определить для любого состояния, в том числе **InsufficientThroughput**.

```PowerShell
PS C:\> Get-StorageQosFlow -Status InsufficientThroughput | fl

FilePath           : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX
FlowId             : 1ca356ff-fd33-5b5d-b60a-2c8659dc803e
InitiatorId        : 2ceabcef-2eba-4f1b-9e66-10f960b50bbf
InitiatorIOPS      : 12168
InitiatorLatency   : 22.983
InitiatorName      : WinOltp1
InitiatorNodeName  : plang-c1.plang.nttest.microsoft.com
Interval           : 300000
Limit              : 20000
PolicyId           : 5d1bf221-c8f0-4368-abcf-aa139e8a7c72
Reservation        : 15000
Status             : InsufficientThroughput
StorageNodeIOPS    : 12181
StorageNodeLatency : 22.0514
StorageNodeName    : plang-fs2.plang.nttest.microsoft.com
TimeStamp          : 2/13/2015 12:07:30 PM
VolumeId           : 0d2fd367-8d74-4146-9934-306726913dda
PSComputerName     :
MaximumIops        : 20000
MinimumIops        : 15000
```

## <a name="monitor-health-using-storage-qos"></a><a name="BKMK_Health"></a>Мониторинг состояния работоспособности с помощью службы качества обслуживания хранилища
Новая служба работоспособности упрощает мониторинг кластера хранилища за счет централизованной проверки на наличие событий, требующих применения действий, на любом узле. В этом разделе описывается, как отслеживать работоспособность кластера хранилища с помощью командлета `debug-storagesubsystem`.

### <a name="view-storage-status-with-debug-storagesubsystem"></a>Просмотр состояния хранилища с помощью командлета Debug-StorageSubSystem
Сведения о работоспособности кластера хранилища в одном расположении можно также просмотреть с помощью кластерного дискового пространства. Это может помочь администраторам быстро определить проблемы при развертываниях хранилищ, а также отслеживать появление и устранение проблем.

#### <a name="vm-with-invalid-policy"></a>Виртуальные машины с недопустимыми политиками
Недопустимые политики виртуальных машин также обнаруживаются при мониторинге работоспособности подсистемы хранения.  Ниже приведен пример с тем же состоянием, что и в разделе [Определение виртуальных машин с недопустимыми политиками](#BKMK_FindingVMsWithInvalidPolicies) этой статьи.

```PowerShell
C:\> Get-StorageSubSystem -FriendlyName Clustered* | Debug-StorageSubSystem

EventTime                 :
FaultId                   : 0d16d034-9f15-4920-a305-f9852abf47c3
FaultingObject            :
FaultingObjectDescription : Storage QoS Policy 5d1bf221-c8f0-4368-abcf-aa139e8a7c72
FaultingObjectLocation    :
FaultType                 : Storage QoS policy used by consumer does not exist.
PerceivedSeverity         : Minor
Reason                    : One or more storage consumers (usually Virtual Machines) are
                            using a non-existent policy with id
                            5d1bf221-c8f0-4368-abcf-aa139e8a7c72. Consumer details:

                            Flow ID: 1ca356ff-fd33-5b5d-b60a-2c8659dc803e
                            Initiator ID: 2ceabcef-2eba-4f1b-9e66-10f960b50bbf
                            Initiator Name: WinOltp1
                            Initiator Node: plang-c1.plang.nttest.microsoft.com
                            File Path:
                            C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX
RecommendedActions        : {Reconfigure the storage consumers (usually Virtual Machines)
                            to use a valid policy., Recreate any missing Storage QoS
                            policies.}
PSComputerName            :
```

#### <a name="lost-redundancy-for-a-storage-spaces-virtual-disk"></a>Потеря избыточности виртуального диска, входящего в дисковое пространство

В этом примере в кластерное дисковое пространство добавлен виртуальный диск, созданный как трехстороннее зеркало.  Из системы удалили отказавший диск, но другой диск не добавили.  Подсистема хранения сообщает о потере избыточности, выдавая значение **Warning** для свойства HealthStatus, но, поскольку том все еще подключен, свойство OperationalStatus имеет значение **OК**.

```PowerShell
PS C:\> Get-StorageSubSystem -FriendlyName Clustered*

FriendlyName                   HealthStatus                   OperationalStatus
------------                   ------------                   -----------------
Clustered Windows Storage o... Warning                        OK

[plang-fs1]: PS C:\Users\plang\Documents> Get-StorageSubSystem -FriendlyName Clustered* | Deb
ug-StorageSubSystem

EventTime                 :
FaultId                   : dfb4b672-22a6-4229-b2ed-c29d7485bede
FaultingObject            :
FaultingObjectDescription : Virtual disk 'Two'
FaultingObjectLocation    :
FaultType                 : VirtualDiskDegradedFaultType
PerceivedSeverity         : Minor
Reason                    : Virtual disk 'Two' does not have enough redundancy remaining to
                            successfully repair or regenerate its data.
RecommendedActions        : {Rebalance the pool, replace failed physical disks, or add new
                            physical disks to the storage pool, then repair the virtual
                            disk.}
PSComputerName            :
```

### <a name="sample-script-for-continuous-monitoring-of-storage-qos"></a>Пример скрипта для обеспечения непрерывного мониторинга качества обслуживания хранилища

В этом разделе также содержится пример скрипта для мониторинга распространенных ошибок с помощью скрипта WMI.  С него разработчики могут начать извлечение событий работоспособности в режиме реального времени.

**Пример скрипта:**

```PowerShell
param($cimSession)
# Register and display events
Register-CimIndicationEvent -Namespace root\microsoft\windows\storage -ClassName msft_storagefaultevent -CimSession $cimSession

while ($true)
{
     $e = (Wait-Event)
     $e.SourceEventArgs.NewEvent
     Remove-Event $e.SourceIdentifier
}
```

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы

### <a name="how-do-i-retain-a-storage-qos-policy-being-enforced-for-my-virtual-machine-if-i-move-its-vhdvhdx-files-to-another-storage-cluster"></a>Как сохранить политику качества обслуживания хранилища, примененную к виртуальной машине, после перемещения ее VHD- или VHDX-файлов в другой кластер хранилища

Для указания политики в VHD- или VHDX-файле используется GUID идентификатора политики.  При создании политики GUID можно задать с помощью параметра **PolicyID**.  Если этот параметр не указан, создается случайный GUID.  Поэтому можно просмотреть идентификатор политики в кластере хранилища, где на данный момент хранятся VHD- и VHDX-файлы виртуальной машины, а затем создать идентичную политику в целевом кластере хранилища и указать ей тот же GUID.  При переносе файлов виртуальной машины в новые кластеры хранилища вступит в силу политика с тем же самым GUID.

Для применения политик к нескольким кластерам хранилища можно использовать System Center Virtual Machine Manager, за счет чего этот сценарий становится намного удобней.
### <a name="if-i-change-the-storage-qos-policy-why-dont-i-see-it-take-effect-immediately-when-i-run-get-storageqosflow"></a>Почему после изменения политики качества обслуживания хранилища и выполнения командлета Get-StorageQoSFlow она сразу же не вступила в силу

Если у вас есть поток, который использует максимальное значение ресурсов, определенное в политике, а затем вы изменяете политику и с помощью командлетов PowerShell сразу же определяете задержку, число операций ввода-вывода в секунду и пропускную способность, то политика вступит в силу в течение 5 минут после изменения.  Новые ограничения вступят в силу в течение нескольких секунд, но командлет PowerShell **Get-StorgeQoSFlow** использует средние значения каждого счетчика в рамках пятиминутного скользящего окна.  В противном случае, если отображалось текущее значение и вы выполнили командлет PowerShell несколько раз подряд, полученные значения могут отличаться. Это связано с тем, что значения операций ввода-вывода и задержки могут меняться каждую секунду.

### <a name="what-new-functionality-was-added-in-windows-server-2016"></a><a name="BKMK_Updates"></a>Какие новые функциональные возможности были добавлены в Windows Server 2016

В Windows Server 2016 имена типов политики качества обслуживания хранилища были изменены.  **Многоэкземплярная** политика изменена на **выделенную**, а **одноэкземплярная** — на **объединенную**. Управление выделенными политиками также изменено. VHD- и VHDX-файлы с одинаковой **выделенной** политикой, расположенные на одной и той же виртуальной машине, не будут иметь общее выделенное число операций ввода-вывода.

В Windows Server 2016 имеются две новые возможности качества обслуживания хранилища:

-   **Максимальная пропускная способность**

    Представленный в Windows Server 2016 компонент качества обслуживания хранилища позволяет указать максимальную пропускную способность, потребляемую потоками, которые назначены политике.  В командлетах **StorageQosPolicy** это параметр **MaximumIOBandwidth**, выходные данные которого выражаются в байтах в секунду.
    Если задать в политике значения **MaximimIops** и **MaximumIOBandwidth**, они оба будут действительными. В этом случае число операций ввода-вывода для потоков определяет первое достигнутое ими значение.

-   **Возможность настройки нормализации для операций ввода-вывода в секунду**

    Компонент качества обслуживания хранилища поддерживает возможность нормализации операций ввода-вывода в секунду.  По умолчанию размер одной нормализованной операции — 8 КБ.  Представленный в Windows Server 2016 компонент качества обслуживания хранилища позволяет указывать для кластера хранилища разный размер одной нормализированной операции.  Этот размер влияет на все потоки в кластере хранилища и применяется непосредственно после изменения значения (в течение нескольких секунд).  Минимальное значение — 1 КБ, максимальное — 4 ГБ (мы не рекомендуем устанавливать более 4 МБ, так как обычно в рамках одной операции ввода-вывода не передается более 4 МБ данных).

    Обратите внимание, что при изменении значения нормализации операций ввода-вывода в секунду в выходных данных компонента качества обслуживания хранилища после измерения числа операций ввода-вывода и пропускной способности будет отображаться разное число IOPS. Это связано с изменением расчета нормализации.  При сравнении числа операций ввода-вывода в секунду в разных кластерах хранилища просмотрите значение нормализации в каждом из них, так как это имеет значение при определении числа нормализованных операций ввода-вывода в секунду.

#### <a name="example-1-creating-a-new-policy-and-viewing-the-maximum-bandwidth-on-the-storage-cluster"></a>Пример 1. Создание новой политики и просмотр максимальной пропускной способности в кластере хранилища
В PowerShell можно указать единицы измерения.  В следующем примере максимальное значение пропускной способности — 10 МБ.  Компонент качества обслуживания хранилища преобразует это значение и сохранит в байтах в секунду (10 МБ равно 10 485 760 байтам в секунду).

```PowerShell
PS C:\Windows\system32> New-StorageQosPolicy -Name HR_VMs -MaximumIops 1000 -MinimumIops 20 -MaximumIOBandwidth 10MB

Name   MinimumIops MaximumIops MaximumIOBandwidth Status
----   ----------- ----------- ------------------ ------
HR_VMs 20          1000        10485760           Ok

PS C:\Windows\system32> Get-StorageQosPolicy

Name    MinimumIops MaximumIops MaximumIOBandwidth Status
----    ----------- ----------- ------------------ ------
Default 0           0           0                  Ok
HR_VMs  20          1000        10485760           Ok

PS C:\Windows\system32> Get-StorageQoSFlow | fL InitiatorName,FilePath,InitiatorIOPS,InitiatorLatency,InitiatorBandwidth

InitiatorName      : testsQoS
FilePath           : C:\ClusterStorage\Volume2\TESTSQOS\VIRTUAL HARD DISKS\TESTSQOS.VHDX
InitiatorIOPS      : 5
InitiatorLatency   : 1.5455
InitiatorBandwidth : 37888
```

#### <a name="example-2-get-iops-normalization-settings-and-specify--a-new-value"></a>Пример 2. Настройка параметров нормализации операций ввода-вывода в секунду и указание нового значения

В следующем примере показано, как настроить нормализацию операций ввода-вывода в секунду для кластеров хранилища (по умолчанию — 8 КБ), задать для этого параметра значение 32 КБ, а затем снова показать его.  Обратите внимание, что, так как PowerShell позволяет не преобразовывать значения в байты, в этом примере можно указать значение 32 КБ.   В выходных данных значение будет отображаться в байтах в секунду.

```PowerShell
PS C:\Windows\system32> Get-StorageQosPolicyStore

IOPSNormalizationSize
---------------------
8192

PS C:\Windows\system32> Set-StorageQosPolicyStore -IOPSNormalizationSize 32KB
PS C:\Windows\system32> Get-StorageQosPolicyStore

IOPSNormalizationSize
---------------------
32768
```

## <a name="see-also"></a>См. также:
- [Windows Server 2016](../../index.yml)
- [Реплика хранилища в Windows Server 2016](../storage-replica/storage-replica-overview.md)
- [Локальные дисковые пространства в Windows Server 2016](../storage-spaces/storage-spaces-direct-overview.md)