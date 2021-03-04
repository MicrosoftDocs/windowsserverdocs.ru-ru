---
title: Управление мостом центра обработки данных (DCB)
description: В этом разделе приведены инструкции по использованию команд Windows PowerShell для управления мостом центра обработки данных в Windows Server 2016.
ms.topic: article
ms.assetid: 1575cc7c-62a7-4add-8f78-e5d93effe93f
manager: brianlic
ms.author: jgerend
author: JasonGerend
ms.date: 12/08/2020
ms.openlocfilehash: 95613a9656945213c1e22ad14085a50c75a4aa63
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101833813"
---
# <a name="manage-data-center-bridging-dcb"></a>Управление мостом центра обработки данных (DCB)

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе приведены инструкции по использованию команд Windows PowerShell для настройки моста карт для центра обработки данных \( \) в \- сетевом адаптере, совместимом с DCB, установленным на компьютере под управлением Windows Server 2016 или Windows 10.

## <a name="install-dcb-in-windows-server-2016-or-windows-10"></a>Установка DCB в Windows Server 2016 или Windows 10

Сведения о предварительных требованиях для использования и установке DCB см. [в разделе Установка моста центра обработки данных (DCB) в Windows Server 2016 или Windows 10](dcb-install.md).


## <a name="dcb-configurations"></a>Конфигурации DCB

До выхода Windows Server 2016 вся конфигурация DCB была применена глобально ко всем сетевым адаптерам, которые поддерживали DCB.

В Windows Server 2016 можно применять конфигурации DCB либо к глобальному хранилищу политик, либо к отдельному хранилищу политик \( \) . При применении отдельных политик они переопределяют все глобальные параметры политики.

Конфигурации класса трафика, распределения коэффициента мощности и приоритета приложения на уровне системы не применяются к сетевым адаптерам до тех пор, пока не будут выполнены следующие действия.

1. Установите бит ДКБКС в значение false.

2. Включите DCB на сетевых адаптерах. См. раздел [Включение и отображение параметров DCB на сетевых адаптерах](#bkmk_enabledcb).

>[!NOTE]
>Если вы хотите настроить DCB из коммутатора с помощью ДКБКС, см. раздел [дкбкс Settings](#dcb-configuration-on-network-adapters).

Бит ДКБКС, который Вы раздаете, описывается в спецификации DCB. Если для параметра bit на устройстве задано значение true, устройство может принимать конфигурации с удаленного устройства через ДКБКС. Если в качестве бита на устройстве задано значение false, устройство будет отклонять все попытки настройки с удаленных устройств и применять только локальные конфигурации.

Если DCB не установлен в Windows Server 2016, значение параметра bit не имеет значения, что касается операционной системы, так как в операционной системе нет локальных параметров, применяемых к сетевым адаптерам. После установки DCB значение по умолчанию для параметра bit устанавливается равным true. Такая схема позволяет сетевым адаптерам оставаться в любых конфигурациях, которые они могли получить от своих удаленных одноранговых узлов.

Если сетевой адаптер не поддерживает ДКБКС, он никогда не будет принимать конфигурации с удаленного устройства. Он получает конфигурации от операционной системы, но только после того, как в качестве бита ДКБКСа будет установлено значение false.

## <a name="set-the-willing-bit"></a>Установка бита

Чтобы применить конфигурации операционной системы для класса трафика, коэффициента мощности и назначения приоритета приложений для сетевых адаптеров или просто переопределить конфигурации с удаленных устройств \ — если есть, можно выполнить следующую команду.

>[!NOTE]
>Имена команд Windows PowerShell DCB включают в себя "QoS" вместо "DCB" в строке имени. Это обусловлено тем, что службы QoS и DCB интегрированы в Windows Server 2016 для обеспечения беспрепятственного управления качества обслуживания.

```powershell
    Set-NetQosDcbxSetting -Willing $FALSE

    Confirm
    Are you sure you want to perform this action?
    Set-NetQosDcbxSetting -Willing $false
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
```

Чтобы отобразить состояние параметра "разрешается", можно использовать следующую команду:

```powershell
    Get-NetQosDcbxSetting

    Willing PolicySetIfIndex IfAlias
    ------- ---------------- -------
    False   Global
```

## <a name="dcb-configuration-on-network-adapters"></a>Конфигурация DCB на сетевых адаптерах

Включение DCB на сетевом адаптере позволяет увидеть конфигурацию, распространенную с коммутатора на сетевой адаптер.

Конфигурации DCB включают следующие шаги.

1.  Настройте параметры DCB на уровне системы, включая:

    а. Управление классами трафика

    b. Параметры управления потоком приоритета (коэффициент мощности)

    c. Назначение приоритета приложения

    d. Параметры ДКБКС

2. Настройте DCB на сетевом адаптере.

##  <a name="dcb-traffic-class-management"></a>Управление классами трафика DCB

Ниже приведены примеры команд Windows PowerShell для управления классами трафика.

### <a name="create-a-traffic-class"></a>Создание класса трафика

Для создания класса трафика можно использовать команду **New-неткостраффиккласс** .

```powershell
    New-NetQosTrafficClass -Name SMB -Priority 4 -BandwidthPercentage 30 -Algorithm ETS

    Name Algorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ---- --------- ------------ -------- ---------------- -------
    SMB  ETS   30   4Global
```

По умолчанию все значения 802.1 p сопоставляются с классом трафика по умолчанию, который имеет 100% пропускной способности физической связи. Команда **New-неткостраффиккласс** создает новый класс трафика, с которым сопоставляется любой пакет, помеченный с помощью значения 802.1 p Priority с приоритетом 4. Алгоритм выбора передачи \( TSA \) является ETS и имеет 30% пропускной способности.

Можно создать до 7 новых классов трафика. Включая класс трафика по умолчанию, в системе может быть не более 8 классов трафика. Однако сетевой адаптер с поддержкой DCB может не поддерживать такое количество классов трафика на оборудовании. Если вы создаете больше классов трафика, чем может разместиться на сетевом адаптере, и включаете DCB на этом сетевом адаптере, драйвер минипорта сообщает об ошибке в операционной системе. Эта ошибка заносится в журнал событий.

Сумма резервирования пропускной способности для всех созданных классов трафика не может превышать 99% от пропускной способности. Класс трафика по умолчанию всегда имеет по крайней мере 1% от пропускной способности, зарезервированной для себя.

### <a name="display-traffic-classes"></a>Отображение классов трафика

Для просмотра классов трафика можно использовать команду **Get-неткостраффиккласс** .

```powershell
    Get-NetQosTrafficClass

    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   70   0-3,5-7  Global
    SMB ETS   30   4Global
```

### <a name="modify-a-traffic-class"></a>Изменение класса трафика

Для создания класса трафика можно использовать команду **Set-неткостраффиккласс** .

```powershell
    Set-NetQosTrafficClass -Name SMB -BandwidthPercentage 50
```

Затем можно использовать команду **Get-неткостраффиккласс** для просмотра параметров.

```powershell
    Get-NetQosTrafficClass

    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   50   0-3,5-7  Global
    SMB ETS   50   4Global
```

После создания класса трафика его параметры можно изменить независимо. Можно изменить следующие параметры:

1. Распределение пропускной способности (-Бандвидсперцентаже)

2. TSA (-Algorithm)

3. Сопоставление приоритетов (-Priority)

### <a name="remove-a-traffic-class"></a>Удаление класса трафика

Для удаления класса трафика можно использовать команду **Remove-неткостраффиккласс** .

>[!IMPORTANT]
>Нельзя удалить класс трафика по умолчанию.

```powershell
    Remove-NetQosTrafficClass -Name SMB

You can then use the **Get-NetQosTrafficClass** command to view settings.

    Get-NetQosTrafficClass

    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   100  0-7  Global
```

После удаления класса трафика значение 802.1 p, сопоставленное с этим классом трафика, повторно сопоставляется с классом трафика по умолчанию. Любая пропускная способность, зарезервированная для класса трафика, возвращается к выделению класса трафика по умолчанию при удалении класса трафика.

## <a name="per-network-interface-policies"></a>Политики интерфейса Per-Network

Все приведенные выше примеры задают глобальные политики. Ниже приведены примеры того, как можно задать и получить политики для каждого сетевого адаптера.

Поле "Policy" («политика») меняется с Global на АдаптерспеЦифик. При отображении политик АдаптерспеЦифик также отображаются индекс интерфейса \( ifIndex \) и имя интерфейса \( ифалиас \) .

```powershell
PS C:\> Get-NetQosTrafficClass

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       100          0-7              Global


PS C:\> Get-NetQosTrafficClass -InterfaceAlias M1

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       100          0-7              AdapterSpecific  4       M1


PS C:\> New-NetQosTrafficClass -Name SMBGlobal -BandwidthPercentage 30 -Priority 4 -Algorithm ETS

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
SMBGlobal   ETS       30           4                Global


PS C:\> New-NetQosTrafficClass -Name SMBforM1 -BandwidthPercentage 30 -Priority 4 -Algorithm ETS -Interfac


Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
SMBforM1    ETS       30           4                AdapterSpecific  4       M1


PS C:\> Get-NetQosTrafficClass

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       70           0-3,5-7          Global
SMBGlobal   ETS       30           4                Global


PS C:\> Get-NetQosTrafficClass -InterfaceAlias M1

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       70           0-3,5-7          AdapterSpecific  4       M1
SMBforM1    ETS       30           4                AdapterSpecific  4       M1

```

## <a name="priority-flow-control-settings"></a>Параметры управления потоком приоритета:

Ниже приведены примеры команд для параметров управления потоком приоритета. Эти параметры также можно указать для отдельных адаптеров.

### <a name="enable-and-display-priority-flow-control-for-global-and-interface-specific-use-cases"></a>Включение и отображение управления потоком приоритета для глобальных вариантов использования и конкретных интерфейсов

```powershell
PS C:\> Enable-NetQosFlowControl -Priority 4
PS C:\> Enable-NetQosFlowControl -Priority 3 -InterfaceAlias M1
PS C:\> Get-NetQosFlowControl

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      Global
1          False      Global
2          False      Global
3          False      Global
4          True       Global
5          False      Global
6          False      Global
7          False      Global

PS C:\> Get-NetQosFlowControl -InterfaceAlias M1

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      AdapterSpecific  4       M1
1          False      AdapterSpecific  4       M1
2          False      AdapterSpecific  4       M1
3          True       AdapterSpecific  4       M1
4          False      AdapterSpecific  4       M1
5          False      AdapterSpecific  4       M1
6          False      AdapterSpecific  4       M1
7          False      AdapterSpecific  4       M1
```

### <a name="disable-priority-flow-control-global-and-interface-specific"></a>Отключить управление потоком приоритета (для глобальных и особых интерфейсов)

```powershell
PS C:\> Disable-NetQosFlowControl -Priority 4
PS C:\> Disable-NetQosFlowControl -Priority 3 -InterfaceAlias m1
PS C:\> Get-NetQosFlowControl

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      Global
1          False      Global
2          False      Global
3          False      Global
4          False      Global
5          False      Global
6          False      Global
7          False      Global

PS C:\> Get-NetQosFlowControl -InterfaceAlias M1

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      AdapterSpecific  4       M1
1          False      AdapterSpecific  4       M1
2          False      AdapterSpecific  4       M1
3          False      AdapterSpecific  4       M1
4          False      AdapterSpecific  4       M1
5          False      AdapterSpecific  4       M1
6          False      AdapterSpecific  4       M1
7          False      AdapterSpecific  4       M1
```

##  <a name="application-priority-assignment"></a>Назначение приоритета приложения

Ниже приведены примеры назначения приоритета.

### <a name="create-qos-policy"></a>Создание политики качества обслуживания

```powershell
PS C:\> New-NetQosPolicy -Name "SMB Policy" -SMB -PriorityValue8021Action 4

Name           : SMB Policy
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
Template       : SMB
PriorityValue  : 4
```

Предыдущая команда создает новую политику для SMB. — SMB — это фильтр входящих сообщений, соответствующий TCP-порту 445 (зарезервировано для SMB). Если пакет отправляется на TCP-порт 445, он будет помечен операционной системой со значением 802.1 p, равным 4, перед передачей пакета драйверу минипорта сети.

Помимо SMB, другие фильтры по умолчанию включают – iSCSI (соответствующий TCP-порт 3260),-NFS (соответствующий TCP-порт 2049),-Ливемигратион (соответствующий TCP-порт 6600),-ФКОЕ (сопоставление Есертипе 0x8906) и – Нетворкдирект.

Нетворкдирект — это абстрактный слой, создаваемый на основе любой реализации RDMA на сетевом адаптере. – За Нетворкдирект должен следовать сетевой прямой порт.

Помимо фильтров по умолчанию трафик можно классифицировать по имени исполняемого файла приложения (как в первом примере ниже) или по IP-адресу, порту или протоколу (как показано во втором примере):

**По имени исполняемого файла**

```powershell
PS C:\> New-NetQosPolicy -Name background -AppPathNameMatchCondition "C:\Program files (x86)\backup.exe" -PriorityValue8021Action 1

Name           : background
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
AppPathName    : C:\Program files (x86)\backup.exe
JobObject      :
PriorityValue  : 1
```

**По порту или протоколу IP-адреса**

```powershell
PS C:\> New-NetQosPolicy -Name "Network Management" -IPDstPrefixMatchCondition 10.240.1.0/24 -IPProtocolMatchCondition both -NetworkProfile all -PriorityValue8021Action 7

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7
```

### <a name="display-qos-policy"></a>Отображение политики качества обслуживания

```powershell
PS C:\> Get-NetQosPolicy

Name           : background
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
AppPathName    : C:\Program files (x86)\backup.exe
JobObject      :
PriorityValue  : 1

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7

Name           : SMB Policy
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
Template       : SMB
JobObject      :
PriorityValue  : 4
```

### <a name="modify-qos-policy"></a>Изменение политики качества обслуживания

Вы можете изменить политики качества обслуживания, как показано ниже.

```powershell
PS C:\> Set-NetQosPolicy -Name "Network Management" -IPSrcPrefixMatchCondition 10.235.2.0/24 -IPProtocolMatchCondition both -PriorityValue8021Action 7
PS C:\> Get-NetQosPolicy

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPSrcPrefix    : 10.235.2.0/24
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7
```

### <a name="remove-qos-policy"></a>Удалить политику качества обслуживания

```powershell
PS C:\> Remove-NetQosPolicy -Name "Network Management"

Confirm
Are you sure you want to perform this action?
Remove-NetQosPolicy -Name "Network Management" -Store GPO:localhost
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="dcb-configuration-on-network-adapters"></a>Конфигурация DCB на сетевых адаптерах

Конфигурация DCB на сетевых адаптерах не зависит от конфигурации DCB на системном уровне, описанном выше.

Независимо от того, установлена ли в Windows Server 2016 DCB, вы всегда можете выполнить следующие команды.

Если настроить DCB с коммутатора и использовать ДКБКС для распространения конфигураций на сетевые адаптеры, то после включения DCB на сетевых адаптерах можно узнать, какие конфигурации будут получены и применены на сетевых адаптерах, начиная с операционной системы.

###  <a name="enable-and-display-dcb-settings-on--network-adapters"></a><a name="bkmk_enabledcb"></a>Включение и отображение параметров DCB на сетевых адаптерах

```powershell
PS C:\> Enable-NetAdapterQos M1
PS C:\> Get-NetAdapterQos

Name                       : M1
Enabled                    : True
Capabilities               :                       Hardware     Current
                                                   --------     -------
                             MacSecBypass        : NotSupported NotSupported
                             DcbxSupport         : None         None
                             NumTCs(Max/ETS/PFC) : 8/8/8        8/8/8

OperationalTrafficClasses  : TC TSA    Bandwidth Priorities
                             -- ---    --------- ----------
                              0 ETS    70%       0-3,5-7
                              1 ETS    30%       4

OperationalFlowControl     : All Priorities Disabled
OperationalClassifications : Protocol  Port/Type Priority
                             --------  --------- --------
                             Default             1
```

### <a name="disable-dcb-on-network-adapters"></a>Отключение DCB на сетевых адаптерах

```powershell
PS C:\> Disable-NetAdapterQos M1
PS C:\> Get-NetAdapterQos M1

Name         : M1
Enabled      : False
Capabilities :                       Hardware     Current
                                     --------     -------
               MacSecBypass        : NotSupported NotSupported
               DcbxSupport         : None         None
               NumTCs(Max/ETS/PFC) : 8/8/8        0/0/0
```

## <a name="windows-powershell-commands-for-dcb"></a><a name="bkmk_wps"></a>Команды Windows PowerShell для DCB

Существуют команды Windows PowerShell для Windows Server 2016 и Windows Server 2012 R2. Вы можете использовать все команды для Windows Server 2012 R2 в Windows Server 2016.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Команды Windows PowerShell для Windows Server 2016 для DCB

В следующем разделе для Windows Server 2016 приведены описания и синтаксис командлетов Windows PowerShell для всех командлетов качества обслуживания центра обработки данных, \( \) \( связанных с QoS \) \- . Командлеты перечисляются в алфавитном порядке по команде в начале имени командлета.

- [Модуль Дкбкос](/powershell/module/dcbqos/)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>Команды Windows PowerShell для Windows Server 2012 R2 для DCB

В следующем разделе для Windows Server 2012 R2 приведены описания и синтаксис командлетов Windows PowerShell для всех командлетов качества обслуживания центра обработки данных, \( \) \( связанных с QoS \) \- . Командлеты перечисляются в алфавитном порядке по команде в начале имени командлета.

- [Командлеты качества обслуживания моста для центра обработки данных в Windows PowerShell](/powershell/module/dcbqos/)
