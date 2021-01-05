---
title: Развертывание сервера Nano Server
description: Сведения о создании и развертывании настраиваемых образов, пакетов, драйверов, доменов, ролей и функций
manager: DonGill
ms.date: 09/06/2017
ms.topic: conceptual
ms.assetid: 9f109c91-7c2e-4065-856c-ce9e2e9ce558
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: e2a60a3fdb27753784773659711f486421ed31b3
ms.sourcegitcommit: 5f234fb15c1d0365b60e83a50bf953e317d6239c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97879853"
---
# <a name="deploy-nano-server"></a>Развертывание сервера Nano Server

> Область применения. Windows Server 2016

> [!IMPORTANT]
> Начиная с Windows Server версии 1709, сервер Nano Server будет доступен только в качестве [базового образа ОС контейнера](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image). Его описание см. в статье об [изменениях сервера Nano Server](nano-in-semi-annual-channel.md).

Этот раздел содержит сведения, необходимые для развертывания образов сервера Nano Server, которые в большей степени настроены под ваши потребности, чем простые примеры из раздела "Краткое руководство по серверу Nano Server". Вы найдете сведения о создании пользовательского образа сервера Nano Server с нужными возможностями, установке образов Nano Server из VHD или WIM, редактировании файлов, работе с доменами, нескольких способах обработки пакетов и работе с ролями сервера.

## <a name="nano-server-image-builder"></a>Nano Server Image Builder

Nano Server Image Builder — это средство, которое позволяет создать пользовательский образ Nano Server и загрузочный USB-носитель с помощью графического интерфейса. В зависимости от предоставленных вами входных данных оно создает повторно используемый сценарий PowerShell, позволяющий легко автоматизировать согласованные установки Nano Server под управлением выпуска Windows Server 2016 Datacenter или Standard.

Скачайте средство из [Центра загрузки](https://www.microsoft.com/download/details.aspx?id=54065).

Этому средству также требуется [комплект средств для развертывания и оценки Windows (ADK)](https://developer.microsoft.comwindows/hardware/windows-assessment-deployment-kit).

Nano Server Image Builder создает настроенные образы Nano Server в формате VHD, VHDX или ISO и позволяет создать загрузочный USB-носитель для развертывания Nano Server или обнаружения конфигураций оборудования сервера. Это средство также может выполнять следующие действия:

- Принятие условий лицензионного соглашения.
- Создание файлов в формате VHD, VHDX или ISO.
- Добавление ролей сервера.
- Добавление драйверов устройств.
- Задание имени компьютера, пароля администратора, пути к журналу и часового пояса.
- Присоединение к домену с использованием существующей учетной записи Active Directory или полученного большого двоичного объекта присоединения к домену.
- Включение WinRM для взаимодействия вне локальной подсети.
- Включение идентификаторов виртуальных локальных сетей и настройка статических IP-адресов.
- Внедрение новых пакетов обслуживания в режиме реального времени.
- Добавление setupcomplete.cmd или другого сценария клиента для выполнения после обработки unattend.xml.
- Включение служб аварийного управления (EMS) для доступа к консоли через последовательный порт.
- Включение служб разработки для включения драйверов с тестовой подписью и неподписанных приложений, оболочки PowerShell по умолчанию.
- Включение отладки через последовательный порт, USB, протоколы TCP/IP или IEEE 1394.
- Создание USB-носителя с помощью среды предустановки Windows, который разделит сервер на разделы и установит образ Nano.
- Создание USB-носителя с помощью среды предустановки Windows, который обнаружит существующую аппаратную конфигурацию Nano Server и выведет все сведения в журнале и на экране. Сюда входят сетевые адаптеры, MAC-адреса и тип встроенного ПО (BIOS или UEFI). Процесс обнаружения также выведет список всех томов в системе и устройств, на которых нет драйвера, включенного в пакет драйверов основных серверных компонентов.

Если вам незнаком любой из этих аспектов, просмотрите этот раздел и другие разделы о Nano Server, чтобы предоставить средству необходимые сведения.

## <a name="creating-a-custom-nano-server-image"></a><a name=BKMK_CreateImage></a>Создание пользовательского образа Nano Server

Для Windows Server 2016 компонент Nano Server размещается на физическом носителе, где находится папка **NanoServer** с WIM-образом и вложенной папкой **Packages**. Это файлы пакетов, позволяющие добавить компоненты и роли сервера в образ виртуального жесткого диска, с которого затем осуществляется загрузка.

Можно также найти и установить эти пакеты с помощью поставщика NanoServerPackage модуля PackageManagement (OneGet) для PowerShell. См. раздел "Установка ролей и компонентов в сети" этой статьи.

В этой таблице показаны роли и функции, доступные в этом выпуске Nano Server, а также параметры Windows PowerShell, которые установят пакеты для них. Некоторые пакеты устанавливаются непосредственно со своими собственными параметрами Windows PowerShell (такими как -Compute), другие устанавливаются посредством передачи имен пакетов в параметр -Package, который можно объединить в список с разделителями-запятыми. Список доступных пакетов можно формировать динамически с помощью командлета Get-NanoServerPackage.

| Роль или компонент | Параметр |
|--|--|
| Роль Hyper-V (включая NetQoS) | -Compute |
| Отказоустойчивая кластеризация и другие компоненты, подробное описание после этой таблицы | -Clustering |
| Базовые драйверы для различных сетевых адаптеров и контроллеров устройств хранения. Это тот же набор драйверов, который включен в установку основных серверных компонентов для Windows Server 2016. | -OEMDrivers |
| Роль файлового сервера и другие компоненты хранилища, подробное описание после этой таблицы | -Storage |
| Защитник Windows, включая файл сигнатур по умолчанию | -Defender |
| Серверы обратной пересылки для обеспечения совместимости приложений, например общие платформы приложений, такие как Ruby, Node.js и т. д. | Теперь включено по умолчанию |
| Роль DNS-сервера | -Package Microsoft-NanoServer-DNS-Package |
| PowerShell Desired State Configuration (DSC) | -Package Microsoft-NanoServer-DSC-Package<p>**Примечание**. Дополнительные сведения см. в статье [Использование DSC на сервере Nano Server](/archive/blogs/askcore/kms-host-client-count-not-increasing-due-to-duplicate-cmids). |
| Службы IIS | -Package Microsoft-NanoServer-IIS-Package<p>**Примечание**. Сведения о работе с IIS см. в разделе [IIS на сервере Nano Server](IIS-on-Nano-Server.md). |
| Поддержка узлов для контейнеров Windows | -Containers |
| Агент System Center Virtual Machine Manager | -Package Microsoft-NanoServer-SCVMM-Package<p>-Package Microsoft-NanoServer-SCVMM-Compute-Package<p>**Примечание**. Используйте пакет вычислений SCVMM только в том случае, если отслеживаете Hyper-V. Для гиперконвергентных развертываний в VMM также нужно указать параметр -Storage. Дополнительные сведения см. в [документации по VMM](/system-center/vmm/hyper-v-nano?view=sc-vmm-2016&preserve-view=true). |
| Агент System Center Operations Manager | Устанавливается отдельно. Дополнительные сведения см. в документации по System Center Operations Manager: https://technet.microsoft.com/system-center-docs/om/manage/install-agent-on-nano-server. |
| Мост для центра обработки данных (включая DCBQoS) | -Package Microsoft-NanoServer-DCB-Package |
| Развертывание на виртуальной машине | -Package Microsoft-NanoServer-Guest-Package |
| Развертывание на физическом компьютере | -Package Microsoft-NanoServer-Host-Package |
| BitLocker, доверенный платформенный модуль (TPM), шифрование тома, идентификация платформы, поставщики служб шифрования и другие функции, связанные с безопасным запуском | -Package Microsoft-NanoServer-SecureStartup-Package |
| Поддержка экранированных виртуальных машин в Hyper-V | -Package Microsoft-NanoServer-ShieldedVM-Package<p>**Примечание**. Этот пакет доступен только для выпуска Datacenter сервера Nano Server. |
| Агент протокола SNMP | -Package Microsoft-NanoServer-SNMP-Agent-Package.cab<p>**Примечание**. Не содержится на установочном носителе Windows Server 2016. Доступна только в Интернете. Дополнительные сведения см. в разделе [Установка ролей и компонентов в сети](#BKMK_online). |
| Служба IPHelper, которая обеспечивает возможность туннельного подключения с помощью технологий туннелирования для IPv6 (6to4, ISATAP, Port Proxy и Teredo) и IP-HTTP. | -Package Microsoft-NanoServer-IPHelper-Service-Package.cab<p>**Примечание**. Не содержится на установочном носителе Windows Server 2016. Доступна только в Интернете. Дополнительные сведения см. в разделе [Установка ролей и компонентов в сети](#BKMK_online). |

> [!NOTE]
> При установке пакетов с этими параметрами также устанавливается соответствующий языковой пакет в зависимости от языкового стандарта носителя для выбранного сервера. Доступные языковые пакеты и их сокращения языкового стандарта находятся на установочном носителе во вложенных папках, у которых в качестве имени используется языковой стандарт образа.

> [!NOTE]
> При установке файловых служб с использованием параметра -Storage эти службы не включаются. Включите эту функцию с удаленного компьютера с помощью диспетчера сервера.

### <a name="failover-clustering-items-installed-by-the--clustering-parameter"></a>Элементы отказоустойчивой кластеризации, которые устанавливаются при использовании параметра -Clustering

- Роль отказоустойчивой кластеризации
- Отказоустойчивая кластеризация виртуальной машины
- Локальные дисковые пространства (S2D)
- Качество обслуживания хранилища
- Кластеризация при репликации томов
- Служба-свидетель SMB

### <a name="file-and-storage-items-installed-by-the--storage-parameter"></a>Файлы и элементы хранилища, установленные при использовании параметра -Storage

- Роль файлового сервера
- дедупликация данных;
- Multipath I/O, в том числе драйвер для специального модуля для устройств Майкрософт (MSDSM)
- ReFS (версия 1 и 2)
- Инициатор iSCSI (но не целевой объект iSCSI)
- Реплика хранилища
- Служба управления хранением данных с поддержкой SMI-S
- Служба-свидетель SMB
- Динамические тома
- Основные поставщики хранилища Windows (для управления хранилищами Windows)

### <a name="installing-a-nano-server-vhd"></a>Установка виртуального жесткого диска Nano Server

В этом примере создается образ VHDX на основе GPT с заданным именем компьютера, включающий гостевые драйверы Hyper-V и запускаемый с установочного носителя Nano Server на общем сетевом ресурсе. В командной строке Windows PowerShell с повышенными привилегиями начните с этого командлета:

```powershell
Import-Module <Server media location>\NanoServer\NanoServerImageGenerator; New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\server_en-us -BasePath .\Base -TargetPath .\FirstStepsNano.vhdx -ComputerName FirstStepsNano
```

Этот командлет выполнит все следующие задачи:

1. Выбор Standard в качестве базового выпуска.

2. Запрос пароля администратора у пользователя.

3. Копирование установочного носителя из \\\Path\To\Media\server_en-us в .\Base

4. Преобразование WIM-образа в виртуальный жесткий диск. (Расширение файла в аргументе целевого пути определяет, создается ли VHD на основе MBR для виртуальных машин поколения 1 или VHDX на основе GPT для виртуальных машин поколения 2.)

5. Копирование полученного VHD в .\FirstStepsNano.vhdx

6. Задание пароля администратора для образа в указанном виде.

7. Задание для имени компьютера образа значения FirstStepsNano.

8. Установка гостевых драйверов Hyper-V.

Все это приводит к созданию образа .\FirstStepsNano.vhdx.

Во время работы командлет создает журнал. О расположении этого журнала вы узнаете после его завершения. Для преобразования из WIM в VHD, осуществляемого вспомогательным сценарием, создается собственный журнал в расположении %TEMP%\Convert-WindowsImage\\\<GUID> (где \<GUID> — это уникальный идентификатор для сеанса преобразования).

Пока вы используете тот же базовый путь, можно опустить параметр пути носителя при каждом запуске этого командлета, так как он будет применять кэшированные файлы из базового пути. Если базовый путь не указан, командлет создает путь по умолчанию в папке TEMP. Если вы хотите использовать другой исходный носитель, но тот же базовый путь, параметр пути к носителю нужно задать.

> [!NOTE]
> Теперь у вас есть возможность указать создаваемый выпуск Nano Server — Standard или Datacenter. Используйте параметр -Edition для указания выпусков *Standard* или *Datacenter*.

При наличии существующего образа можно внести в него необходимые изменения с помощью командлета *Edit-NanoServerImage*.

Если имя компьютера не указано, будет создано случайное имя.

### <a name="installing-a-nano-server-wim"></a>Установка WIM Nano Server

1. Скопируйте папку *NanoServerImageGenerator* из папки \NanoServer ISO-образа Windows Server 2016 в локальную папку на компьютере.
2. Запустите Windows PowerShell с правами администратора, перейдите в папку, куда скопировали NanoServerImageGenerator, а затем импортируйте модуль с помощью `Import-Module .\NanoServerImageGenerator -Verbose`.

   >[!NOTE]
   >Может потребоваться настроить политику выполнения Windows PowerShell. `Set-ExecutionPolicy RemoteSigned` должен подойти.

Чтобы создать образ Nano Server, используемый в качестве узла Hyper-V, выполните следующую команду:

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerPhysical\NanoServer.wim -ComputerName <computer name> -OEMDrivers -Compute -Clustering`
```

Где
- MediaPath является корнем DVD-диска или ISO-образа, содержащего Windows Server 2016.
- `-BasePath` будет содержать копию двоичных файлов Nano Server, чтобы вы могли использовать New-NanoServerImage -BasePath без указания -MediaPath в последующих запусках.
- `-TargetPath` будет содержать результирующий WIM-файл с выбранными ролями и компонентами. Обязательно укажите расширение WIM.
- `-Compute` позволяет добавить роль Hyper-V.
- `-OemDrivers` позволяет добавить несколько распространенных драйверов.

Вы получите приглашение ввести пароль администратора.

Чтобы получить дополнительные сведения, запустите `Get-Help New-NanoServerImage -Full`.

Загрузитесь в среде предустановки Windows и убедитесь, что из нее доступен созданный WIM-файл. (Можно например, скопировать WIM-файл в загрузочный образ среды предустановки Windows на USB-устройстве флэш-памяти.)

После загрузки среды предустановки Windows используйте Diskpart.exe для подготовки жесткого диска на конечном компьютере. Выполните следующие команды Diskpart (изменив их соответствующим образом, если UEFI и GPT не используются):

> [!WARNING]
> При выполнении этих команд удаляются все данные на жестком диске:

  ```
  Diskpart.exe
  Select disk 0
  Clean
  Convert GPT
  Create partition efi size=100
  Format quick FS=FAT32 label=System
  Assign letter=s
  Create partition msr size=128
  Create partition primary
  Format quick FS=NTFS label=NanoServer
  Assign letter=n
  List volume
  Exit
  ```

Примените образ Nano Server (изменив путь к WIM-файлу):

```
Dism.exe /apply-image /imagefile:.\NanoServer.wim /index:1 /applydir:n:\
Bcdboot.exe n:\Windows /s s:
```

Извлеките DVD-диск или USB-накопитель и перезагрузите систему с помощью команды **Wpeutil.exe reboot**.

### <a name="editing-files-on-nano-server-locally-and-remotely"></a>Локальное и удаленное изменение файлов на Nano Server

В любом случае подключитесь к Nano Server, например, с помощью удаленного взаимодействия Windows PowerShell.

После подключения к Nano Server можно изменить файл, расположенный на локальном компьютере, передав относительный или абсолютный путь файла в команду psEdit, например: `psEdit C:\Windows\Logs\DISM\dism.log` или `psEdit .\myScript.ps1`.

Измените файл, расположенный на удаленном сервере Nano Server, запустив удаленный сеанс с помощью `Enter-PSSession -ComputerName 192.168.0.100 -Credential ~\Administrator` и передав относительный или абсолютный путь файла в команду psEdit следующим образом: `psEdit C:\Windows\Logs\DISM\dism.log`.

## <a name="installing-roles-and-features-online"></a><a name=BKMK_online></a>Установка ролей и компонентов в сети

> [!NOTE]
> Если устанавливается необязательный пакет Nano Server с носителя или из интернет-репозитория, он не будет содержать последних исправлений безопасности. Чтобы избежать несоответствия версий дополнительных пакетов и базовой операционной системы, [последний накопительный пакет обновления](./update-nano-server.md) следует установить сразу после установки любых дополнительных пакетов и **перед** перезапуском сервера.

### <a name="installing-roles-and-features-from-a-package-repository"></a>Установка ролей и компонентов из репозитория пакетов

Пакеты Nano Server можно найти и установить из интернет-репозитория пакетов с помощью поставщика NanoServerPackage модуля PackageManagement для PowerShell. Чтобы установить этот поставщик, используйте следующие командлеты:

```powershell
Install-PackageProvider NanoServerPackage
Import-PackageProvider NanoServerPackage
```

>[!NOTE]
>Если возникают ошибки при запуске Install-PackageProvider, проверьте, установлен ли [последний накопительный пакет обновления](./update-nano-server.md) ([KB3206632](https://support.microsoft.com/kb/3206632) или новее), или воспользуйтесь командлетом Save-Module, как показано ниже.

```powershell
Save-Module -Path $Env:ProgramFiles\WindowsPowerShell\Modules\ -Name NanoServerPackage -MinimumVersion 1.0.1.0
Import-PackageProvider NanoServerPackage
```

После установки и импорта этого поставщика вы можете найти, скачать и установить пакеты Nano Server с помощью командлетов, созданных специально для работы с пакетами Nano Server:

```powershell
Find-NanoServerPackage
Save-NanoServerPackage
Install-NanoServerPackage
```

Вы также можете использовать универсальные командлеты PackageManagement и указать поставщик NanoServerPackage:

```powershell
Find-Package -ProviderName NanoServerPackage
Save-Package -ProviderName NanoServerPackage
Install-Package -ProviderName NanoServerPackage
Get-Package -ProviderName NanoServerPackage
```

Чтобы использовать любой из этих командлетов с пакетами Nano Server на сервере Nano Server, добавьте `-ProviderName NanoServerPackage`. Если не добавить параметр -ProviderName, PackageManagement выполнит перебор всех поставщиков. Для получения дополнительных сведений об этих командлетах выполните `Get-Help <cmdlet>`. Ниже приведены распространенные примеры использования.

### <a name="searching-for-nano-server-packages"></a>Поиск пакетов Nano Server

Вы можете использовать `Find-NanoServerPackage` или `Find-Package -ProviderName NanoServerPackage` для поиска пакетов Nano Server, доступных в интернет-репозитории, и возврата их списка. Например, можно получить список всех последних пакетов:

```powershell
Find-NanoServerPackage
```

Если выполнить `Find-Package -ProviderName NanoServerPackage -DisplayCulture`, будут показаны все доступные языки и региональные параметры.

Если нужна конкретная версия языкового стандарта, например английский (США), можно использовать `Find-NanoServerPackage -Culture en-us`, `Find-Package -ProviderName NanoServerPackage -Culture en-us` или `Find-Package -Culture en-us -DisplayCulture`.

Чтобы найти пакет по имени, используйте параметр -Name. Этот параметр также принимает подстановочные знаки. Например, чтобы найти все пакеты с аббревиатурой VMM в имени, используйте `Find-NanoServerPackage -Name *VMM*` или `Find-Package -ProviderName NanoServerPackage -Name *VMM*`.

Можно найти определенную версию с помощью параметров -RequiredVersion, -MinimumVersion или -MaximumVersion. Чтобы найти все доступные версии, используйте - AllVersions. В противном случае возвращается только последняя версия. Например: `Find-NanoServerPackage -Name *VMM* -RequiredVersion 10.0.14393.0`. Или для всех версий: `Find-Package -ProviderName NanoServerPackage -Name *VMM* -AllVersions`

### <a name="installing-nano-server-packages"></a>Установка пакетов Nano Server

Вы можете установить пакет Nano Server (включая его пакеты зависимостей при их наличии) на Nano Server локально либо в автономном образе с помощью `Install-NanoServerPackage` или `Install-Package -ProviderName NanoServerPackage`. Оба командлета принимают входные данные из конвейера.

Чтобы установить последнюю версию пакета Nano Server на сервере Nano Server в сети, используйте `Install-NanoServerPackage -Name Microsoft-NanoServer-Containers-Package` или `Install-Package -Name Microsoft-NanoServer-Containers-Package`. PackageManagement будет использовать язык и региональные параметры сервера Nano Server.

Пакет Nano Server можно установить в автономный образ, указав конкретную версию и язык следующим образом:

`Install-NanoServerPackage -Name Microsoft-NanoServer-DCB-Package -Culture de-de -RequiredVersion 10.0.14393.0 -ToVhd C:\MyNanoVhd.vhd`

или:

`Install-Package -Name Microsoft-NanoServer-DCB-Package -Culture de-de -RequiredVersion 10.0.14393.0 -ToVhd C:\MyNanoVhd.vhd`

Ниже приведено несколько примеров конвейерной обработки результатов поиска пакета для командлета установки:

`Find-NanoServerPackage *dcb* | Install-NanoServerPackage` находит все пакеты с dcb в имени, а затем устанавливает их.

`Find-Package *nanoserver-compute-* | Install-Package` находит все пакеты с nanoserver-compute- в имени, а затем устанавливает их.

`Find-NanoServerPackage -Name *nanoserver-compute* | Install-NanoServerPackage -ToVhd C:\MyNanoVhd.vhd` находит пакеты с compute в имени и устанавливает их в автономный образ.

`Find-Package -ProviderName NanoserverPackage *nanoserver-compute-* | Install-Package -ToVhd C:\MyNanoVhd.vhd` делает то же самое с любым пакетом, в имени которого есть nanoserver-compute-.

### <a name="downloading-nano-server-packages"></a>Скачивание пакетов Nano Server

`Save-NanoServerPackage` или `Save-Package` позволяет скачать и сохранить пакеты без установки. Оба командлета принимают входные данные из конвейера.

Например, чтобы скачать и сохранить пакет Nano Server в каталог, который совпадает с путем с подстановочными знаками, используйте `Save-NanoServerPackage -Name Microsoft-NanoServer-DNS-Package -Path C:\`. В этом примере параметр -Culture не указан, поэтому используются язык и региональные параметры локального компьютера. Версия не указана, поэтому сохраняется последняя версия.

`Save-Package -ProviderName NanoServerPackage -Name Microsoft-NanoServer-IIS-Package -Path C:\ -Culture it-IT -MinimumVersion 10.0.14393.0` сохраняет определенную версию для итальянского языка и языкового стандарта.

Результаты поиска можно отправить через конвейер, как показано в этих примерах:

`Find-NanoServerPackage -Name *containers* -MaximumVersion 10.2 -MinimumVersion 1.0 -Culture es-ES | Save-NanoServerPackage -Path C:\`

,

`Find-Package -ProviderName NanoServerPackage -Name *shield* -Culture es-ES | Save-Package -Path`

### <a name="inventory-installed-packages"></a>Инвентаризация установленных пакетов

Узнать, какие именно пакеты Nano Server установлены, можно с помощью `Get-Package`. Например, просмотрите пакеты на сервере Nano Server с помощью `Get-Package -ProviderName NanoserverPackage`.

Чтобы проверить пакеты Nano Server, установленные в автономном образе, запустите `Get-Package -ProviderName NanoserverPackage -FromVhd C:\MyNanoVhd.vhd`.

### <a name="installing-roles-and-features-from-local-source"></a>Установка ролей и компонентов из локального источника

Хотя для ролей сервера и других пакетов рекомендуется автономная установка, в сценариях с контейнерами может потребоваться установить их в сети (с Nano Server). Для этого выполните следующие действия:

1. Скопируйте папку Packages с установочного носителя на запущенный сервер Nano Server (например, в C:\packages).

2. Создайте файл Unattend.xml на другом компьютере и скопируйте его на сервер Nano Server. Можете скопировать и вставить это содержимое в созданный XML-файл (в примере показана установка пакета IIS):

  ```
  <?xml version=1.0 encoding=utf-8?>
      <unattend xmlns=urn:schemas-microsoft-com:unattend>
      <servicing>
          <package action=install>
              <assemblyIdentity name=Microsoft-NanoServer-IIS-Feature-Package version=10.0.14393.0 processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral />
              <source location=c:\packages\Microsoft-NanoServer-IIS-Package.cab />
          </package>
          <package action=install>
              <assemblyIdentity name=Microsoft-NanoServer-IIS-Feature-Package version=10.0.14393.0 processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=en-US />
              <source location=c:\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab />
          </package>
      </servicing>
      <cpi:offlineImage cpi:source= xmlns:cpi=urn:schemas-microsoft-com:cpi />
  </unattend>
  ```

3. В новом XML-файле, который вы создали (или скопировали), измените C:\packages на каталог, куда вы скопировали содержимое папки Packages.

4. Перейдите в каталог с недавно созданным XML-файлом и выполните команду `dism /online /apply-unattend:.\unattend.xml`.

5. Убедитесь, что пакет и связанный с ним языковой пакет установлены правильно, выполнив команду `dism /online /get-packages`.

   Вы должны увидеть идентификатор пакета: Microsoft-NanoServer-IIS-Package~31bf3856ad364e35~amd64~en-US~10.0.10586.0, указанный дважды (для элементов "Тип выпуска: Языковый пакет" и "Тип выпуска: Пакет функций".

## <a name="customizing-an-existing-nano-server-vhd"></a>Настройка существующего виртуального жесткого диска Nano Server

Сведения о существующем виртуальном жестком диске можно изменить с помощью командлета Edit-NanoServerImage, как показано в следующем примере: `Edit-NanoServerImage   -BasePath .\Base   -TargetPath .\BYOVHD.vhd`.

Этот командлет выполняет те же операции, что и New-NanoServerImage, но при этом изменяет существующий образ вместо преобразования WIM в VHD. Он поддерживает те же параметры, что и New-NanoServerImage, за исключением -MediaPath и -MaxSize, поэтому следует создать исходный виртуальный жесткий диск с помощью этих параметров, прежде чем можно будет вносить изменения в Edit-NanoServerImage.

## <a name="additional-tasks-you-can-accomplish-with-new-nanoserverimage-and-edit-nanoserverimage"></a>Дополнительные задачи, которые можно выполнить с помощью New-NanoServerImage и Edit-NanoServerImage

### <a name="joining-domains"></a>Присоединение к доменам

New-NanoServerImage предлагает два способа присоединения к домену. Они оба используют автономную подготовку домена, но один из них получает большой двоичный объект для выполнения присоединения. В этом примере командлет получает большой двоичный объект для домена Contoso с локального компьютера (который, конечно же, должен быть частью домена Contoso), а затем выполняет автономную подготовку образа с помощью этого объекта:

`New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\JoinDomHarvest.vhdx -ComputerName JoinDomHarvest -DomainName Contoso`

После выполнения этого командлета в списке компьютеров Active Directory должен появиться компьютер с именем JoinDomHarvest.

Этот командлет можно также использовать на компьютере, который не присоединен к домену. Для этого получите большой двоичный объект с любого компьютера, присоединенного к домену, и самостоятельно предоставьте этот объект командлету. Обратите внимание, что после получения такого большого двоичного объекта с другого компьютера он уже включает в себя имя этого компьютера. Поэтому при попытке добавить параметр *-ComputerName* возникнет ошибка.

BLOB-объект можно получить с помощью следующей команды:

```
djoin
/Provision
/Domain Contoso
/Machine JoiningDomainsNoHarvest
/SaveFile JoiningDomainsNoHarvest.djoin
```

Запустите New-NanoServerImage с использованием полученного BLOB-объекта:

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\JoinDomNoHrvest.vhd -DomainBlobPath .\Path\To\Domain\Blob\JoinDomNoHrvestContoso.djoin`

Если в домене уже есть узел с таким же именем компьютера, как и ваш будущий Nano Server, можно использовать это имя повторно, добавив параметр `-ReuseDomainNode`.

### <a name="adding-additional-drivers"></a>Добавление дополнительных драйверов

Nano Server предлагает пакет, который включает набор базовых драйверов для различных сетевых адаптеров и контроллеров устройств хранения. Вполне возможно, что драйверы для ваших сетевых адаптеров в него не входят. С помощью приведенных здесь действий можно найти драйверы в работающей системе, извлечь их и затем добавить в образ Nano Server.

1. Установите Windows Server 2016 на физическом компьютере, где будет работать Nano Server.
2. Откройте диспетчер устройств и определите устройства в следующих категориях:
3. Сетевые адаптеры
4. Контроллеры устройств хранения
5. Диски
6. Для каждого устройства в этих категориях щелкните правой кнопкой мыши имя и выберите **Свойства**. В открывшемся диалоговом окне выберите вкладку **Драйвер**, а затем щелкните **Сведения о драйвере**.
7. Запомните отображаемое имя файла и путь к файлу драйвера. Например, предположим, что файл драйвера имеет имя e1i63x64.sys и находится в C:\Windows\System32\Drivers.
8. В командной строке выполните поиск файла драйвера и найдите все экземпляры с dir e1i*.sys /s /b. В этом примере файл драйвера также находится в папке C:\Windows\System32\DriverStore\FileRepository\net1ic64.inf_amd64_fafa7441408bbecd\e1i63x64.sys.
9. В командной строке с повышенными привилегиями перейдите в каталог, где находится виртуальный жесткий диск Nano Server, и выполните следующие команды:

  ```
  md mountdir
  dism\dism /Mount-Image /ImageFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir
  dism\dism /Add-Driver /image:.\mountdir /driver: C:\Windows\System32\DriverStore\FileRepository\net1ic64.inf_amd64_fafa7441408bbecd
  dism\dism /Unmount-Image /MountDir:.\MountDir /Commit
  ```

10. Повторите эти шаги для каждого файла драйвера, который вам нужен.

> [!NOTE]
> В папке, где хранятся драйверы, должны присутствовать как SYS-файлы, так и соответствующие им INF-файлы. Кроме того, Nano Server поддерживает только подписанные 64\-разрядные драйверы.

### <a name="injecting-drivers"></a>Внедрение драйверов

Nano Server предлагает пакет, который включает набор базовых драйверов для различных сетевых адаптеров и контроллеров устройств хранения. Вполне возможно, что драйверы для ваших сетевых адаптеров в него не входят. Чтобы заставить New-NanoServerImage найти доступные драйверы в каталоге и внедрить их в образ Nano Server, можно использовать следующий синтаксис:

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\InjectingDrivers.vhdx -DriverPath .\Extra\Drivers`

> [!NOTE]
> В папке, где хранятся драйверы, должны присутствовать как SYS-файлы, так и соответствующие им INF-файлы. Кроме того, Nano Server поддерживает только подписанные 64-разрядные драйверы.

Используя параметр -DriverPath, можно также передать массив путей в INF-файлы драйверов:

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\InjectingDrivers.vhdx -DriverPath .\Extra\Drivers\netcard64.inf`

### <a name="connecting-with-winrm"></a>Соединение с помощью WinRM

Чтобы иметь возможность подключиться к компьютеру Nano Server с помощью службы удаленного управления Windows (WinRM) (с компьютера в другой подсети), откройте порт 5985 для входящего трафика TCP для образа Nano Server. Используйте следующий командлет:

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\ConnectingOverWinRM.vhd -EnableRemoteManagementPort`

### <a name="setting-static-ip-addresses"></a>Настройка статических IP-адресов

Чтобы настроить образ Nano Server для применения статических IP-адресов, найдите имя или индекс интерфейса, который требуется изменить, используя Get-NetAdapter, netsh или агент восстановления Nano Server. Используйте параметры -Ipv6Address, -Ipv6Dns, -Ipv4Address, -Ipv4SubnetMask, -Ipv4Gateway и -Ipv4Dns для задания конфигурации, как показано в следующем примере:

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\StaticIpv4.vhd -InterfaceNameOrIndex Ethernet -Ipv4Address 192.168.1.2 -Ipv4SubnetMask 255.255.255.0 -Ipv4Gateway 192.168.1.1 -Ipv4Dns 192.168.1.1`

### <a name="custom-image-size"></a>Размер пользовательского образа

Образ Nano Server можно сделать динамически расширяемым VHD или VHDX с помощью параметра -MaxSize, как показано в следующем примере:

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\BigBoss.vhd -MaxSize 100GB`

### <a name="embedding-custom-data"></a>Внедрение пользовательских данных

Чтобы внедрить собственные двоичные файлы или сценарий в образ Nano Server, используйте параметр -CopyPath для передачи массива файлов и каталогов для копирования. Параметр -CopyPath также может принять хэш-таблицу для указания конечного пути файлов и каталогов.

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\BigBoss.vhd -CopyPath .\tools`

### <a name="running-custom-commands-after-the-first-boot"></a>Выполнение пользовательских команд после первой загрузки

Для выполнения пользовательских команд в рамках setupcomplete.cmd используйте параметр -SetupCompleteCommand, чтобы передать массив команд:

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -SetupCompleteCommand @(echo foo, echo bar)`

### <a name="running-custom-powershell-scripts-as-part-of-image-creation"></a>Выполнение пользовательских сценариев PowerShell при создании образов

Для выполнения пользовательских сценариев PowerShell во время создания образа используйте параметр -OfflineScriptPath, чтобы передать массив путей в PS1-сценарии. Если эти сценарии принимают аргументы, используйте параметр -OfflineScriptArgument, чтобы передать хэш-таблицу дополнительных аргументов в сценарии.

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -OfflineScriptPath C:\MyScripts\custom.ps1 -OfflineScriptArgument @{Param1=Value1; Param2=Value2}`

### <a name="support-for-development-scenarios"></a>Поддержка сценариев разработки

Если вы хотите осуществлять разработку и тестирование на базе Nano Server, можно использовать параметр -Development. Это позволит сделать PowerShell локальной оболочкой по умолчанию, устанавливать неподписанные драйверы, копировать двоичные файлы отладчика, открыть порт для отладки, включить тестовую подпись и установку пакетов AppX без лицензии разработчика:

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -Development`

### <a name="custom-unattend-file"></a>Пользовательский файл автоматической установки

Если вы хотите использовать собственный файл автоматической установки, укажите параметр -UnattendPath:

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -UnattendPath \\path\to\unattend.xml`

Задание пароля администратора или имени компьютера в этом файле автоматической установки переопределяет значения, заданные параметрами -AdministratorPassword и -ComputerName.

> [!NOTE]
> Сервер Nano Server не поддерживает настройку параметров TCP/IP с помощью файлов автоматической установки. Вы можете использовать Setupcomplete.cmd, чтобы настроить параметры TCP/IP.

### <a name="collecting-log-files"></a>Сбор файлов журнала

Если вы хотите собрать файлы журнала во время создания образа, используйте параметр -LogPath, чтобы указать каталог, в который копируются файлы.

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -LogPath C:\Logs`

> [!NOTE]
> Некоторые параметры командлетов New-NanoServerImage и NanoServerImage предназначены только для внутреннего использования, их можно игнорировать. К ним относятся параметры -SetupUI и -Internal.

### <a name="windows-server-app-installer"></a>Установщик приложения Windows Server

Установщик приложений Windows Server (WSA) предоставляет надежный вариант установки для Nano Server. Поскольку установщик Windows (MSI) на сервере Nano Server не поддерживается, WSA также является единственной доступной технологией для установки продуктов сторонних производителей. WSA использует технологию пакетов Windows, предназначенную для безопасной и надежной установки и обслуживания приложений с помощью декларативного манифеста. Он расширяет возможности установщика пакетов приложений Windows для поддержки расширений Windows Server. Единственное ограничение заключается в том, что WSA не поддерживает установку драйверов.

Процедура создания и установки пакета WSA на сервере Nano Server включает шаги как со стороны издателя, так и со стороны потребителя пакета.

Издателю пакета требуется сделать следующее:

1. Установить [пакет SDK для Windows 10](https://developer.microsoft.com/windows/downloads/windows-10-sdk), который включает в себя необходимые инструменты для создания пакета WSA: MakeAppx, MakeCert, Pvk2Pfx, SignTool.
2. Объявить манифест. Следуйте [схеме расширения манифеста WSA](/uwp/schemas/appxpackage/uapmanifestschema/element-serverpreview-extension-manual) для создания файла манифеста AppxManifest.xml.
3. Использовать средство **MakeAppx** для создания пакета WSA.
4. Использовать средства **MakeCert** и **Pvk2Pfx** для создания сертификата, а затем **Signtool** для подписи пакета.

После этого потребителю пакета требуется сделать следующее:

1. Запустить командлет [*Import-Certificate*](/uwp/schemas/appxpackage/uapmanifestschema/element-serverpreview-extension-manual) в PowerShell для импорта сертификата издателя, описанного выше на шаге 4, на сервер Nano Server с certStoreLocation в Cert:\LocalMachine\TrustedPeople. Пример: `Import-Certificate -FilePath .\xyz.cer -CertStoreLocation Cert:\LocalMachine\TrustedPeople`
2. Установить приложение на сервере Nano Server, запустив командлет [**Add-AppxPackage**](/uwp/schemas/appxpackage/uapmanifestschema/element-serverpreview-extension-manual) PowerShell, чтобы установить пакет WSA на Nano Server. Пример: `Add-AppxPackage wsaSample.appx`

#### <a name="additional-resources-for-creating-apps"></a>Дополнительные ресурсы для создания приложений

WSA является серверным расширением технологии пакетов приложений Windows (хотя и не размещается в Microsoft Store). Если вы хотите публиковать приложения с помощью WSA, вы можете узнать о конвейере пакетов приложений из этих разделов:

- [Создание базового манифеста пакета](/uwp/schemas/appxpackage/how-to-create-a-basic-package-manifest)
- [Упаковщик приложений (MakeAppx.exe)](/windows/win32/appxpkg/make-appx-package--makeappx-exe-)
- [Создание сертификата для подписи пакета приложения](/windows/win32/appxpkg/how-to-create-a-package-signing-certificate)
- [SignTool](/windows/win32/seccrypto/signtool)

### <a name="installing-drivers-on-nano-server"></a>Установка драйверов на сервере Nano Server

Драйверы сторонних производителей можно установить на сервере Nano Server с помощью пакетов драйверов INF. К ним относятся самонастраивающиеся пакеты драйверов (PnP) и пакеты драйверов фильтра файловой системы. В настоящее время драйверы сетевого фильтра на сервере Nano Server не поддерживаются.

Пакеты драйверов PnP и фильтра файловой системы должны соответствовать требованиям к универсальному драйверу и правилам его установки, а также общим рекомендациям для пакета драйверов, таким как подпись. Эти сведения приведены в следующих разделах:

- [Подписи драйверов](/windows-hardware/drivers/install/driver-signing)
- [Использование универсального INF-файла](/windows-hardware/drivers/install/using-a-universal-inf-file)

#### <a name="installing-driver-packages-offline"></a>Установка пакетов драйверов в автономном режиме

Поддерживаемые пакеты драйверов можно установить на Nano Server в автономном режиме с помощью командлетов [DISM.exe](/windows-hardware/manufacture/desktop/dism-driver-servicing-command-line-options-s14) или [DISM PowerShell](/powershell/module/dism/add-windowsdriver).

#### <a name="installing-driver-packages-online"></a>Установка пакетов драйверов в сети
Пакеты драйверов PnP можно установить на Nano Server в сети с помощью [PnpUtil](/windows-hardware/drivers/devtest/pnputil). Установка драйвера в сети для пакетов драйверов, отличных от PnP, на Nano Server сейчас не поддерживается.

## <a name="joining-nano-server-to-a-domain"></a><a name=BKMK_JoinDomain></a>Присоединение сервера Nano Server к домену

### <a name="to-add-nano-server-to-a-domain-online"></a>Порядок добавления сервера Nano Server к домену в сети

1. Получите BLOB-объект с компьютера в этом домене, где уже выполняется сервер Windows Threshold, с помощью следующей команды:

    `djoin.exe /provision /domain <domain-name> /machine <machine-name> /savefile .\odjblob`

    При этом BLOB-объект сохраняется в файл с именем odjblob.

2. Скопируйте файл odjblob на компьютер Nano Server с помощью следующих команд:

    **net use z: \\\\\<ip address of Nano Server>\c$**

    > [!NOTE]
    > В случае сбоя команды net use, вероятнее всего, требуется настроить правила брандмауэра Windows. Для этого сначала откройте командную строку с повышенными привилегиями, запустите Windows PowerShell и подключитесь к компьютеру Nano Server с помощью удаленного взаимодействия Windows PowerShell, используя следующие команды:
    >
    > `Set-Item WSMan:\localhost\Client\TrustedHosts <IP address of Nano Server>`
    >
    > `$ip = <ip address of Nano Server>`
    >
    > `Enter-PSSession -ComputerName $ip -Credential $ip\Administrator`
    >
    > При появлении запроса введите пароль администратора, а затем выполните следующую команду, чтобы задать правило брандмауэра:
    >
    > **netsh advfirewall firewall set rule group=File and Printer Sharing new enable=yes**
    >
    > Закройте Windows PowerShell с помощью `Exit-PSSession`, а затем попробуйте выполнить команду net use еще раз. При успешном выполнении продолжите работу, скопировав содержимое файла odjblob на сервер Nano Server.

    **md z:\Temp**

    **copy odjblob z:\Temp**

3. Проверьте домен, к которому нужно присоединить Nano Server, и убедитесь, что служба DNS настроена. Кроме того, убедитесь, что разрешение имен для домена или контроллера домена работает правильно. Для этого откройте командную строку с повышенными привилегиями, запустите Windows PowerShell и подключитесь к компьютеру Nano Server с помощью удаленного взаимодействия Windows PowerShell, используя следующие команды:

    `Set-Item WSMan:\localhost\Client\TrustedHosts <IP address of Nano Server>`

    `$ip = <ip address of Nano Server>`

    `Enter-PSSession -ComputerName $ip -Credential $ip\Administrator`

    При появлении запроса введите пароль администратора. Nslookup недоступна на Nano Server, поэтому разрешение имен можно проверить с помощью Resolve-DNSName.

4. Если разрешение имен выполняется успешно, в том же сеансе Windows PowerShell выполните следующую команду для присоединения к домену:

    `djoin /requestodj /loadfile c:\Temp\odjblob /windowspath c:\windows /localos`

5. Перезапустите компьютер Nano Server и выйдите из сеанса Windows PowerShell:

    `shutdown /r /t 5`

    `Exit-PSSession`

6. После присоединения Nano Server к домену добавьте учетную запись пользователя домена в группу администраторов на сервере Nano Server.

7. Для обеспечения безопасности удалите Nano Server из списка доверенных узлов с помощью следующей команды: `Set-Item WSMan:\localhost\client\TrustedHosts `

**Альтернативный метод для присоединения к домену за один шаг**

Получите BLOB-объект с другого компьютера с запущенным сервером Windows Threshold, который уже находится в вашем домене, с помощью следующей команды:

`djoin.exe /provision /domain <domain-name> /machine <machine-name> /savefile .\odjblob`

Откройте файл odjblob (например, в Блокноте), скопируйте его содержимое и вставьте в раздел \<AccountData> файла Unattend.xml ниже.

Поместите этот файл Unattend.xml в папку C:\NanoServer и выполните следующие команды, чтобы подключить виртуальный жесткий диск и применить параметры в разделе `offlineServicing`:

```
dism\dism /Mount-ImagemediaFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir
dism\dismmedia:.\mountdir /Apply-Unattend:.\unattend.xml
```

Создайте папку Panther (которая используется системами Windows для хранения файлов во время установки; см. раздел [Расположения файлов журнала для программы установки Windows 7, Windows Server 2008 R2 и Windows Vista](https://support.microsoft.com/kb/927521)), скопируйте в нее файл Unattend.xml, а затем отключите виртуальный жесткий диск с помощью следующих команд:

```
md .\mountdir\windows\panther
copy .\unattend.xml .\mountdir\windows\panther
dism\dism /Unmount-Image /MountDir:.\mountdir /Commit
```

При первой загрузке Nano Server из этого виртуального жесткого диска будут применяться другие параметры.

После присоединения Nano Server к домену добавьте учетную запись пользователя домена в группу администраторов на сервере Nano Server.

## <a name="working-with-server-roles-on-nano-server"></a>Работа с ролями сервера на сервере Nano Server

### <a name="using-hyper-v-on-nano-server"></a>Использование Hyper-V на сервере Nano Server

Hyper-V на сервере Nano Server работает точно так же, как и в Windows Server в режиме основных серверных компонентов, с двумя исключениями:

- Все управление необходимо осуществлять удаленно, а на компьютере управления должна выполняться та же сборка Windows Server, что и на сервере Nano Server. Более старые версии командлетов диспетчера Hyper-V или Hyper-V Windows PowerShell работать не будут.

- RemoteFX недоступен.

В этом выпуске были проверены следующие функции Hyper-V:

- Включение Hyper-V

- Создание виртуальных машин поколения 1 и поколения 2

- Создание виртуальных коммутаторов

- Запуск виртуальных машин и использование операционных систем на виртуальной машине

- Реплика Hyper-V

Если вы хотите выполнить динамическую миграцию виртуальных машин, создайте виртуальную машину в общей папке SMB или подключите ресурсы из имеющейся общей папки SMB к существующей виртуальной машине. При этом крайне важно правильно настроить проверку подлинности. Для этого у вас есть два варианта:

**Ограниченное делегирование**

Ограниченное делегирование работает точно так же, как в предыдущих выпусках. Дополнительные сведения см. в следующих статьях:

- [Включение удаленного управления Hyper-V— настройка ограниченного делегирования для SMB и SMB высокой доступности](https://blogs.msdn.com/b/taylorb/archive/2012/03/20/enabling-hyper-v-remote-management-configuring-constrained-delegation-for-smb-and-highly-available-smb.aspx)

- [Включение удаленного управления Hyper-V— настройка ограниченного делегирования для некластеризованной динамической миграции](https://blogs.msdn.com/b/taylorb/archive/2012/03/20/enabling-hyper-v-remote-management-configuring-constrained-delegation-for-non-clustered-live-migration.aspx)

**CredSSP**

Сначала обратитесь к разделу "Использование удаленного взаимодействия Windows PowerShell" этой статьи для включения и тестирования CredSSP. Затем на компьютере управления можно воспользоваться диспетчером Hyper-V и выбрать параметр "Подключиться как другой пользователь". Диспетчер Hyper-V будет использовать CredSSP. Это следует сделать даже при использовании текущей учетной записи.

Командлеты Windows PowerShell для Hyper-V могут использовать параметр CimSession или Credential, которые поддерживают CredSSP.

### <a name="using-failover-clustering-on-nano-server"></a><a name=BKMK_Failover></a>Использование отказоустойчивой кластеризации на сервере Nano Server

Отказоустойчивая кластеризация работает одинаково, что на сервере Nano Server, что в Windows Server в режиме основных серверных компонентов, но следует помнить о следующих особенностях:

- Кластеры должны управляться удаленно, с помощью диспетчера отказоустойчивости кластеров или Windows PowerShell.

- Все узлы кластера Nano Server должны быть присоединены к одному домену по аналогии с узлами кластера в Windows Server.

- Учетная запись домена должна иметь права администратора на всех узлах Nano Server, как и в случае с узлами кластера в Windows Server.

- Все команды необходимо запустить в командной строке с повышенными привилегиями.

> [!NOTE]
> Кроме того, в этом выпуске не поддерживаются некоторые функции:
>
> - Запуск командлетов отказоустойчивой кластеризации на локальном сервере Nano Server с помощью Windows PowerShell.
> - Кластеризация ролей, отличных от Hyper-V и файлового сервера.

Для управления отказоустойчивыми кластерами пригодятся следующие командлеты Windows PowerShell:

Можно создать новый кластер с помощью команды `New-Cluster -Name <clustername> -Node <comma-separated cluster node list>`

После создания кластера следует запустить `Set-StorageSetting -NewDiskPolicy OfflineShared` на всех узлах.

Добавьте дополнительный узел к кластеру с помощью команды `Add-ClusterNode -Name <comma-separated cluster node list>  -Cluster <clustername>`

Удалите узел из кластера с помощью команды `Remove-ClusterNode -Name <comma-separated cluster node list>  -Cluster <clustername>`

Создайте масштабируемый файловый сервер с помощью команды `Add-ClusterScaleoutFileServerRole -name <sofsname> -cluster <clustername>`

Дополнительные командлеты для отказоустойчивой кластеризации можно найти в [Microsoft.FailoverClusters.PowerShell](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee461009(v=technet.10)).

### <a name="using-dns-server-on-nano-server"></a><a name=BKMK_DNS></a>Использование DNS-сервера на сервере Nano Server

Чтобы предоставить Nano Server роль DNS-сервера, добавьте Microsoft-NanoServer-DNS-Package в образ (см. раздел "Создание пользовательского образа Nano Server" этой статьи). После запуска сервера Nano Server подключитесь к нему и запустите следующую команду из консоли Windows PowerShell с повышенными привилегиями, чтобы включить данную функцию:

`Enable-WindowsOptionalFeature -Online -FeatureName DNS-Server-Full-Role`

### <a name="using-iis-on-nano-server"></a><a name=BKMK_IIS></a>Использование служб IIS на сервере Nano Server

Действия для использования роли служб IIS см. в статье [IIS на сервере Nano Server](IIS-on-Nano-Server.md).

### <a name="using-mpio-on-nano-server"></a>Использование MPIO на сервере Nano Server

Действия для использования MPIO см. в статье [MPIO на сервере Nano Server](MPIO-on-Nano-Server.md)

### <a name="using-ssh-on-nano-server"></a><a name=BKMK_SSH></a>Использование SSH на сервере Nano Server

Инструкции по установке и использованию SSH на сервере Nano Server в проекте OpenSSH см. на [вики-сайте по Win32-OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/wiki).

## <a name="appendix-sample-unattendxml-file-that-joins-nano-server-to-a-domain"></a>Приложение. Пример файла Unattend.xml, присоединяющий сервер Nano Server к домену

> [!NOTE]
> Не забудьте удалить пробел в конце содержимого файла odjblob после его вставки в файл автоматической установки.

```xml
<?xml version='1.0' encoding='utf-8'?>
<unattend xmlns=urn:schemas-microsoft-com:unattend xmlns:wcm=https://schemas.microsoft.com/WMIConfig/2002/State xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance>

  <settings pass=offlineServicing>
    <component name=Microsoft-Windows-UnattendedJoin processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral versionScope=nonSxS>
        <OfflineIdentification>
           <Provisioning>
             <AccountData> AAAAAAARUABLEABLEABAoAAAAAAAMABSUABLEABLEABAwAAAAAAAAABbMAAdYABc8ABYkABLAABbMAAEAAAAMAAA0ABY4ABZ8ABbIABa0AAcIABY4ABb8ABZUABAsAAAAAAAQAAZoABNUABOYABZYAANQABMoAAOEAAMIAAOkAANoAAMAAAXwAAJAAAAYAAA0ABY4ABZ8ABbIABa0AAcIABY4ABb8ABZUABLEAALMABLQABU0AATMABXAAAAAAAKdf/mhfXoAAUAAAQAAAAb8ABLQABbMABcMABb4ABc8ABAIAAAAAAb8ABLQABbMABcMABb4ABc8ABLQABb0ABZIAAGAAAAsAAR4ABTQABUAAAAAAACAAAQwABZMAAZcAAUgABVcAAegAARcABKkABVIAASwAAY4ABbcABW8ABQoAAT0ABN8AAO8ABekAAJMAAVkAAZUABckABXEABJUAAQ8AAJ4AAIsABZMABdoAAOsABIsABKkABQEABUEABIwABKoAAaAABXgABNwAAegAAAkAAAAABAMABLIABdIABc8ABY4AADAAAA4AAZ4ABbQABcAAAAAAACAAkKBW0ID8nJDWYAHnBAXE77j7BAEWEkl+lKB98XC2G0/9+Wd1DJQW4IYAkKBAADhAnKBWEwhiDAAAM2zzDCEAM6IAAAgAAAAAAAQAAAAAAAAAAAABwzzAAA
              </AccountData>
           </Provisioning>
         </OfflineIdentification>
    </component>
  </settings>

  <settings pass=oobeSystem>
    <component name=Microsoft-Windows-Shell-Setup processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral versionScope=nonSxS>
      <UserAccounts>
        <AdministratorPassword>
           <Value>Tuva</Value>
           <PlainText>true</PlainText>
        </AdministratorPassword>
      </UserAccounts>
      <TimeZone>Pacific Standard Time</TimeZone>
    </component>
  </settings>

  <settings pass=specialize>
    <component name=Microsoft-Windows-Shell-Setup processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral versionScope=nonSxS>
      <RegisteredOwner>My Team</RegisteredOwner>
      <RegisteredOrganization>My Corporation</RegisteredOrganization>
    </component>
  </settings>
</unattend>
```
