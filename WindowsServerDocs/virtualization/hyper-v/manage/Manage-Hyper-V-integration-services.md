---
title: Управление Integration Services Hyper-V
description: Описывает включение и отключение служб Integration Services и их установку при необходимости
ms.author: benarm
author: BenjaminArmstrong
ms.date: 12/20/2016
ms.topic: article
ms.assetid: 9cafd6cb-dbbe-4b91-b26c-dee1c18fd8c2
ms.openlocfilehash: 8b1519bb8b17393a29a04413eebcae0126799480
ms.sourcegitcommit: 5f234fb15c1d0365b60e83a50bf953e317d6239c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97879883"
---
# <a name="manage-hyper-v-integration-services"></a>Управление Integration Services Hyper-V

> Область применения: Windows 10, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows Server 2019

Hyper-V Integration Services повысить производительность виртуальной машины и предоставить удобные возможности, используя двустороннюю связь с узлом Hyper-V. Многие из этих служб являются удобством, например копированием гостевых файлов, а другие важны для функционирования виртуальной машины, например синтетических драйверов устройств. Этот набор служб и драйверов иногда называют "интеграционными компонентами". Вы можете управлять тем, работают ли отдельные удобные службы для каждой заданной виртуальной машины. Компоненты драйверов не предназначены для обслуживания вручную.

Дополнительные сведения о каждой службе интеграции см. в разделе [Hyper-V Integration Services](/virtualization/hyper-v-on-windows/reference/integration-services).

> [!IMPORTANT]
> Каждая служба, которую необходимо использовать, должна быть включена как на узле, так и в гостевой системе, чтобы обеспечить их функционирование. Все службы Integration Services, кроме "интерфейс гостевой службы Hyper-V", включены по умолчанию в операционных системах Windows на виртуальной машине. Службы можно включать и отключать отдельно. В следующих разделах показано, как это делать.

## <a name="turn-an-integration-service-on-or-off-using-hyper-v-manager"></a>Включение или отключение службы интеграции с помощью диспетчера Hyper-V

1. В центральной области щелкните правой кнопкой мыши виртуальную машину и выберите пункт **Параметры**.

2. В левой области окна **Параметры** в разделе **Управление** щелкните **Integration Services**.

В области Integration Services перечислены все службы Integration Services, доступные на узле Hyper-V, а также указано, разрешено ли для них использование виртуальной машины на узле.

### <a name="turn-an-integration-service-on-or-off-using-powershell"></a>Включение или отключение службы интеграции с помощью PowerShell

Для этого в PowerShell используйте [Enable-VMIntegrationService](/powershell/module/hyper-v/enable-vmintegrationservice) и [Disable-VMIntegrationService](/powershell/module/hyper-v/disable-vmintegrationservice).

В следующих примерах показано, как включить и отключить гостевую службу копирования файлов для виртуальной машины с именем "demovm".

1. Получить список работающих служб Integration Services:

    ``` PowerShell
    Get-VMIntegrationService -VMName "DemoVM"
    ```

1. Выходные данные должны выглядеть так:

    ``` PowerShell
   VMName      Name                    Enabled PrimaryStatusDescription SecondaryStatusDescription
   ------      ----                    ------- ------------------------ --------------------------
   DemoVM      Guest Service Interface False   OK
   DemoVM      Heartbeat               True    OK                       OK
   DemoVM      Key-Value Pair Exchange True    OK
   DemoVM      Shutdown                True    OK
   DemoVM      Time Synchronization    True    OK
   DemoVM      VSS                     True    OK
   ```

1. Включите интерфейс гостевой службы:

   ``` PowerShell
   Enable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
   ```

1. Убедитесь, что интерфейс гостевой службы включен:

   ```
   Get-VMIntegrationService -VMName "DemoVM"
   ```

1. Отключите интерфейс гостевой службы:

    ```
    Disable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
    ```

## <a name="checking-the-guests-integration-services-version"></a>Проверка версии служб интеграции гостя
Некоторые функции могут работать неправильно или вообще, если службы интеграции гостевого компьютера не являются актуальными. Чтобы получить сведения о версии для Windows, выполните вход в операционную систему на виртуальной машине, откройте командную строку и выполните следующую команду:

```
REG QUERY "HKLM\Software\Microsoft\Virtual Machine\Auto" /v IntegrationServicesVersion
```

В предыдущих гостевых операционных системах будут отсутствовать все доступные службы. Например, гости Windows Server 2008 R2 не могут иметь "интерфейс гостевой службы Hyper-V".

## <a name="start-and-stop-an-integration-service-from-a-windows-guest"></a>Запуск и завершение службы интеграции из гостевого компьютера Windows
Для обеспечения полной функциональности службы интеграции соответствующая служба должна быть запущена на гостевом компьютере, а также включена на узле. В Windows Гости каждая служба интеграции указана как стандартная служба Windows. Для отключения и запуска этих служб можно использовать приложение "службы" на панели управления или PowerShell.

> [!IMPORTANT]
> Остановка службы интеграции может серьезно повлиять на возможность узла управлять виртуальной машиной. Для правильной работы каждая служба интеграции, которую вы хотите использовать, должна быть включена как на узле, так и в гостевой системе.
> Рекомендуется управлять службами Integration Services только с помощью Hyper-V, используя приведенные выше инструкции. Служба сопоставления в гостевой операционной системе будет приостановлена или запущена автоматически при изменении ее состояния в Hyper-V.
> Если запустить службу в гостевой операционной системе, но она отключена в Hyper-V, служба будет остановлена. Если вы останавливаете службу в гостевой операционной системе, которая включена в Hyper-V, Hyper-V будет в конечном итоге запустить ее снова. Если отключить службу в гостевой системе, Hyper-V не сможет запустить ее.

### <a name="use-windows-services-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Использование служб Windows для запуска или завершения работы службы интеграции в гостевой системе Windows

1. Откройте диспетчер служб, выполнив ```services.msc``` команду от имени администратора или дважды щелкнув значок службы на панели управления.

    ![Снимок экрана, на котором отображается панель "службы Windows"](media/HVServices.png)

1. Найдите службы, которые начинаются с Hyper-V.

1. Щелкните правой кнопкой мыши службу, которую нужно запустить или прерывать. Щелкните нужное действие.

### <a name="use-windows-powershell-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Использование Windows PowerShell для запуска или завершения работы службы интеграции в гостевой системе Windows

1. Чтобы получить список служб Integration Services, выполните:

    ```
    Get-Service -Name vm*
    ```

1.  Результат должен выглядеть следующим образом:

    ```PowerShell
    Status   Name               DisplayName
    ------   ----               -----------
    Running  vmicguestinterface Hyper-V Guest Service Interface
    Running  vmicheartbeat      Hyper-V Heartbeat Service
    Running  vmickvpexchange    Hyper-V Data Exchange Service
    Running  vmicrdv            Hyper-V Remote Desktop Virtualizati...
    Running  vmicshutdown       Hyper-V Guest Shutdown Service
    Running  vmictimesync       Hyper-V Time Synchronization Service
    Stopped  vmicvmsession      Hyper-V VM Session Service
    Running  vmicvss            Hyper-V Volume Shadow Copy Requestor
    ```

1. Выполните команду [Start-Service](/powershell/module/microsoft.powershell.management/start-service?view=powershell-7&preserve-view=true) или [Service](/powershell/module/microsoft.powershell.management/stop-service?view=powershell-7&preserve-view=true). Например, чтобы отключить Windows PowerShell Direct, выполните команду:

    ```
    Stop-Service -Name vmicvmsession
    ```

## <a name="start-and-stop-an-integration-service-from-a-linux-guest"></a>Запуск и завершение службы интеграции из гостевой ОС Linux

Службы интеграции Linux обычно предоставляются через ядро Linux. Драйвер служб интеграции Linux называется **hv_utils**.

1. Чтобы узнать, загружен ли **hv_utils** , выполните следующую команду:

   ``` BASH
   lsmod | grep hv_utils
   ```

2. Результат должен выглядеть следующим образом:

    ``` BASH
    Module                  Size   Used by
    hv_utils               20480   0
    hv_vmbus               61440   8 hv_balloon,hyperv_keyboard,hv_netvsc,hid_hyperv,hv_utils,hyperv_fb,hv_storvsc
    ```

3. Чтобы узнать, работают ли необходимые управляющие программы, используйте эту команду.

    ``` BASH
    ps -ef | grep hv
    ```

4. Результат должен выглядеть следующим образом:

    ```BASH
    root       236     2  0 Jul11 ?        00:00:00 [hv_vmbus_con]
    root       237     2  0 Jul11 ?        00:00:00 [hv_vmbus_ctl]
    ...
    root       252     2  0 Jul11 ?        00:00:00 [hv_vmbus_ctl]
    root      1286     1  0 Jul11 ?        00:01:11 /usr/lib/linux-tools/3.13.0-32-generic/hv_kvp_daemon
    root      9333     1  0 Oct12 ?        00:00:00 /usr/lib/linux-tools/3.13.0-32-generic/hv_kvp_daemon
    root      9365     1  0 Oct12 ?        00:00:00 /usr/lib/linux-tools/3.13.0-32-generic/hv_vss_daemon
    scooley  43774 43755  0 21:20 pts/0    00:00:00 grep --color=auto hv
    ```

5. Чтобы отобразить все доступные управляющие программы, выполните следующую команду:

    ``` BASH
    compgen -c hv_
    ```

6. Результат должен выглядеть следующим образом:

    ``` BASH
    hv_vss_daemon
    hv_get_dhcp_info
    hv_get_dns_info
    hv_set_ifconfig
    hv_kvp_daemon
    hv_fcopy_daemon
    ```

   Ниже перечислены управляющие программы интеграции, которые могут быть включены в список. Если таковые отсутствуют, они могут не поддерживаться в вашей системе или быть не установлены. Дополнительные сведения см. [в статье Поддерживаемые виртуальные машины Linux и FreeBSD для Hyper-V в Windows](../supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md).
   - **hv_vss_daemon**. Эта управляющая программа необходима для создания динамических резервных копий виртуальных машин Linux.
   - **hv_kvp_daemon**: Эта управляющая программа позволяет задавать и запрашивать внутренние и внешние пары значений ключа.
   - **hv_fcopy_daemon**. Эта управляющая программа реализует службу копирования файлов между узлом и гостем.

### <a name="examples"></a>Примеры

В этих примерах демонстрируется остановка и запуск управляющей программы KVP с именем `hv_kvp_daemon` .

1. \( \) Чтобы предотвратить процесс управляющей программы, используйте идентификатор процесса ID PID. Чтобы найти PID, просмотрите второй столбец выходных данных или используйте `pidof` . Управляющие программы Hyper-V выполняются от имени привилегированного пользователя, поэтому требуются корневые разрешения.

    ``` BASH
    sudo kill -15 `pidof hv_kvp_daemon`
    ```

1. Чтобы убедиться, что все `hv_kvp_daemon` процессы исчезли, выполните:

    ```
    ps -ef | hv
    ```

1. Чтобы запустить управляющую программу еще раз, Запустите управляющую программу от имени root:

    ``` BASH
    sudo hv_kvp_daemon
    ```

1. Чтобы убедиться, что `hv_kvp_daemon` процесс указан с новым идентификатором процесса, выполните команду:

    ```
    ps -ef | hv
    ```

## <a name="keep-integration-services-up-to-date"></a>Обновляйте службы Integration Services в актуальном состоянии

Мы рекомендуем обеспечить актуальность служб Integration Services, чтобы получить максимальную производительность и новейшие функции виртуальных машин. Это происходит для большинства гостей Windows по умолчанию, если они настроены на получение важных обновлений от Центр обновления Windows. Гостевые системы Linux, использующие текущие ядра, получат новейшие компоненты интеграции при обновлении ядра.

**Для виртуальных машин, работающих на узлах Windows 10 или Windows Server 2016/2019, выполните следующие действия.**

> [!NOTE]
> Файл образа vmguest. ISO не входит в Hyper-V в Windows 10 или Windows Server 2016/2019, так как он больше не нужен.

| Гость  | Механизм обновления | Примечания |
|:---------|:---------|:---------|
| быть под управлением ОС Windows 10; | Центра обновления Windows; | |
| Windows 8.1 | Центра обновления Windows; | |
| Windows 8 | Центра обновления Windows; | Требуется служба интеграции для обмена данными.* |
| Windows 7 | Центра обновления Windows; | Требуется служба интеграции для обмена данными.* |
| Windows Vista с пакетом обновления 2 (SP2) | Центра обновления Windows; | Требуется служба интеграции для обмена данными.* |
| - | | |
| Windows Server 2016 | Центра обновления Windows; | |
| Windows Server, Semi-Annual Channel | Центра обновления Windows; | |
| Windows Server 2012 R2 | Центра обновления Windows; | |
| Windows Server 2012 | Центра обновления Windows; | Требуется служба интеграции для обмена данными.* |
| Windows Server 2008 R2 с пакетом обновления 1 (SP1) | Центра обновления Windows; | Требуется служба интеграции для обмена данными.* |
| Windows Server 2008 с пакетом обновления 2 (SP2) | Центра обновления Windows; | Расширенная поддержка только в Windows Server 2016 ([Дополнительные сведения](https://support.microsoft.com/lifecycle?p1=12925)). |
| Windows Home Server 2011 | Центра обновления Windows; | Не будет поддерживаться в Windows Server 2016 ([Дополнительные сведения](https://support.microsoft.com/lifecycle?p1=15820)). |
| Windows Small Business Server 2011 | Центра обновления Windows; | Не в основной фазе поддержки ([подробности](https://support.microsoft.com/lifecycle?p1=15817)). |
| - | | |
| Гостевые ОС Linux | диспетчер пакетов | Службы Integration Services для Linux встроены в дистрибутив, но могут быть доступны необязательные обновления. ******** |

\* Если служба интеграции обмена данными не может быть включена, службы Integration Services для этих гостей доступны в [центре загрузки](https://support.microsoft.com/kb/3071740) в виде CAB-файла. Инструкции по применению CAB-файла доступны в этой [записи блога](https://techcommunity.microsoft.com/t5/virtualization/integration-components-available-for-virtual-machines-not/ba-p/382247).

**Для виртуальных машин, запущенных на узлах Windows 8.1 или Windows Server 2012 R2:**

| Гость  | Механизм обновления | Примечания |
|:---------|:---------|:---------|
| быть под управлением ОС Windows 10; | Центра обновления Windows; | |
| Windows 8.1 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows 8 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows 7 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Vista с пакетом обновления 2 (SP2) | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows XP с пакетами обновления 2 и 3 (SP2, SP3) | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| - | | |
| Windows Server 2016 | Центра обновления Windows; | |
| Windows Server, Semi-Annual Channel | Центра обновления Windows; | |
| Windows Server 2012 R2 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Server 2012 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Server 2008 R2 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Server 2008 с пакетом обновления 2 (SP2) | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Home Server 2011 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Small Business Server 2011 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Server 2003 R2 с пакетом обновления 2 (SP2) | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Server 2003 с пакетом обновления 2 (SP2) | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| - | | |
| Гостевые ОС Linux | диспетчер пакетов | Службы Integration Services для Linux встроены в дистрибутив, но могут быть доступны необязательные обновления. ** |


**Для виртуальных машин, работающих на узлах Windows 8 или Windows Server 2012, выполните следующие действия.**

| Гость  | Механизм обновления | Примечания |
|:---------|:---------|:---------|
| Windows 8.1 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows 8 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows 7 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Vista с пакетом обновления 2 (SP2) | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows XP с пакетами обновления 2 и 3 (SP2, SP3) | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| - | | |
| Windows Server 2012 R2 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Server 2012 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Server 2008 R2 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже.|
| Windows Server 2008 с пакетом обновления 2 (SP2) | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Home Server 2011 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Small Business Server 2011 | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Server 2003 R2 с пакетом обновления 2 (SP2) | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| Windows Server 2003 с пакетом обновления 2 (SP2) | Диск со службами интеграции | См. [инструкции](#install-or-update-integration-services)ниже. |
| - | | |
| Гостевые ОС Linux | диспетчер пакетов | Службы Integration Services для Linux встроены в дистрибутив, но могут быть доступны необязательные обновления. ** |

Дополнительные сведения о гостевых системах Linux см. [в статье Поддерживаемые виртуальные машины Linux и FreeBSD для Hyper-V в Windows](../supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md).

## <a name="install-or-update-integration-services"></a>Установка или обновление служб Integration Services

> [!NOTE]
> Для узлов, предшествующих Windows Server 2016 и Windows 10, необходимо **вручную установить или обновить** службы Integration Services в операционных системах на виртуальной машине.

Процедура установки или обновления служб Integration Services вручную:

1.  Откройте диспетчер Hyper-V. В меню Сервис диспетчер сервера выберите пункт **Диспетчер Hyper-V**.

2.  Подключитесь к виртуальной машине. Щелкните виртуальную машину правой кнопкой мыши и нажмите кнопку **подключить**.

3.  В меню "Действие" подключения к виртуальной машине выберите команду **Вставьте установочный диск служб интеграции**. Это действие загружает установочный диск в виртуальный DVD-дисковод. В зависимости от операционной системы на виртуальной машине может потребоваться запустить установку вручную.

4.  По завершении установки все службы интеграции станут доступны для использования.

> [!NOTE]
> Эти действия **не могут быть автоматизированы** или выполнены в сеансе Windows PowerShell для виртуальных машин в **сети** .
> Их можно применять к **автономным** VHDX-образам. см. раздел [Установка служб Integration Services, если виртуальная машина не запущена](/virtualization/community/team-blog/2013/20130418-how-to-install-integration-services-when-the-virtual-machine-is-not-running).
> Можно также автоматизировать развертывание служб Integration Services с помощью **Configuration Manager** с виртуальными машинами в **сети**, но в конце установки необходимо перезапустить виртуальные машины. см. статью [развертывание Integration Services Hyper-V на виртуальных машинах с помощью диспетчера конфигурации и DISM](/archive/blogs/manageabilityguys/deploying-hyper-v-integration-services-to-vms-using-config-manager-and-dism) .
