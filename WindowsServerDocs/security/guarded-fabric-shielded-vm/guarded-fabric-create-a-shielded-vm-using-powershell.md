---
title: Создание экранированной виртуальной машины с помощью PowerShell
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 09/25/2019
ms.openlocfilehash: 6111b3fbff508c3c485f2a998bab8c0b16beaed6
ms.sourcegitcommit: 471464a674a53c468a2f1e28575c91245ce9badf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/31/2019
ms.locfileid: "75548178"
---
# <a name="create-a-shielded-vm-using-powershell"></a>Создание экранированной виртуальной машины с помощью PowerShell

>Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016

В рабочей среде для развертывания экранированных виртуальных машин обычно используется диспетчер структуры (например, VMM). Однако приведенные ниже действия позволяют развернуть и проверить весь сценарий без диспетчера структуры.

В двух словах, вы создадите диск шаблона, файл данных экранирования, файл ответов автоматической установки и другие артефакты безопасности на любом компьютере, затем скопируйте эти файлы на защищенный узел и подготавливаете экранированную виртуальную машину.

## <a name="create-a-signed-template-disk"></a>Создайте подписанный диск шаблона.

Чтобы создать экранированную виртуальную машину, сначала требуется предварительно зашифрованный диск шаблона виртуальной машины с томом операционной системы (или загрузочными и корневыми разделами в Linux).
Чтобы получить дополнительные сведения о создании диска шаблона, перейдите по приведенным ниже ссылкам.

- [Подготовка диска шаблона Windows](guarded-fabric-create-a-shielded-vm-template.md)
- [Подготовка диска шаблона Linux](guarded-fabric-create-a-linux-shielded-vm-template.md)

Кроме того, для создания файла данных экранирования потребуется копия каталога подписей тома диска.
Чтобы сохранить этот файл, выполните следующую команду на компьютере, где был создан шаблон диска.

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath "C:\temp\MyTemplateDisk.vhdx" -VolumeSignatureCatalogPath "C:\temp\MyTemplateDiskCatalog.vsc"
```

## <a name="download-guardian-metadata"></a>Скачать метаданные опекуна

Для каждой структуры виртуализации, в которой вы хотите запустить экранированную виртуальную машину, необходимо получить метаданные защитника для кластеров HGS.
Поставщик услуг размещения должен иметь возможность предоставлять вам эти сведения.

Если вы используете корпоративную среду и можете взаимодействовать с сервером HGS, метаданные защитника можно найти по адресу *http://\<хгсклустернаме\>/KeyProtection/Service/Metadata/2014-07/Metadata.XML*

## <a name="create-shielding-data-pdk-file"></a>Создание файла данных экранирования (PDK)

Данные экранирования создаются и принадлежат владельцам виртуальных машин клиента и содержат секреты, необходимые для создания экранированных виртуальных машин, которые должны быть защищены от администратора структуры, например пароль администратора экранированной виртуальной машины.
Данные экранирования шифруются таким, что их можно расшифровывать только серверами и клиентами HGS.
После создания владельцем клиента или виртуальной машины полученный PDK-файл должен быть скопирован в защищенную структуру.
Дополнительные сведения см. в разделе [что такое данные экранирования и зачем это необходимо?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary).

Кроме того, потребуется файл ответов автоматической установки (Unattend. XML для Windows, который отличается для Linux). Инструкции по включению в файл ответов см. в разделе [Создание файла ответов](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file) .

Выполните следующие командлеты на компьютере, на котором установлена средства удаленного администрирования сервера для экранированных виртуальных машин.
Если вы создаете PDK для виртуальной машины Linux, это необходимо сделать на сервере под управлением Windows Server версии 1709 или более поздней.

 
```powershell
# Create owner certificate, don't lose this!
# The certificate is stored at Cert:\LocalMachine\Shielded VM Local Certificates
$Owner = New-HgsGuardian –Name 'Owner' –GenerateCertificates
 
# Import the HGS guardian for each fabric you want to run your shielded VM
$Guardian = Import-HgsGuardian -Path C:\HGSGuardian.xml -Name 'TestFabric'
 
# Create the PDK file
# The "Policy" parameter describes whether the admin can see the VM's console or not
# Use "EncryptionSupported" if you are testing out shielded VMs and want to debug any issues during the specialization process
New-ShieldingDataFile -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Owner $Owner –Guardian $guardian –VolumeIDQualifier (New-VolumeIDQualifier -VolumeSignatureCatalogFilePath 'C:\temp\MyTemplateDiskCatalog.vsc' -VersionRule Equals) -WindowsUnattendFile 'C:\unattend.xml' -Policy Shielded
```
    
## <a name="provision-shielded-vm-on-a-guarded-host"></a>Подготавливает экранированную виртуальную машину на защищенном узле
Скопируйте файл шаблона диска (Серверос. VHDX) и PDK-файл (contoso. PDK) на защищенный узел, чтобы подготовиться к развертыванию.

На защищенном узле установите модуль PowerShell для средств защищенной структуры, который содержит командлет New-Шиелдедвм, чтобы упростить процесс подготовки. Если защищенный узел имеет доступ к Интернету, выполните следующую команду:

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

Кроме того, можно загрузить модуль на другой компьютер, имеющий доступ к Интернету, и скопировать полученный модуль в `C:\Program Files\WindowsPowerShell\Modules` на защищенном узле.

```powershell
Save-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0 -Path C:\temp\
```

После установки модуля вы можете подготовить экранированную виртуальную машину.

```powershell
New-ShieldedVM -Name 'MyShieldedVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait
```

Если файл ответов данных экранирования содержит значения специализации, можно предоставить значения замены в New-Шиелдедвм. В этом примере файл ответов настраивается со значениями заполнителей для статического IPv4-адреса.

```powershell
$specializationValues = @{
    "@IP4Addr-1@" = "192.168.1.10/24"
    "@MacAddr-1@" = "Ethernet"
    "@Prefix-1-1@" = "24"
    "@NextHop-1-1@" = "192.168.1.254"
}
New-ShieldedVM -Name 'MyStaticIPVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -SpecializationValues $specializationValues -Wait

```

Если диск шаблона содержит ОС под управлением Linux, включите флаг `-Linux` при выполнении команды:

```powershell
New-ShieldedVM -Name 'MyLinuxVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait -Linux
```

Дополнительные сведения о других параметрах, которые можно передать в командлет, см. в содержимом справки с помощью `Get-Help New-ShieldedVM -Full`.

После завершения подготовки виртуальной машины будет выполнен этап специализации конкретной ОС, после чего он будет готов к использованию.
Не забудьте подключить виртуальную машину к допустимой сети, чтобы можно было подключиться к ней после ее запуска (с помощью RDP, PowerShell, SSH или предпочтительного средства управления).

## <a name="running-shielded-vms-on-a-hyper-v-cluster"></a>Запуск экранированных виртуальных машин в кластере Hyper-V

Если вы пытаетесь развернуть экранированные виртуальные машины на кластеризованных защищенных узлах (с помощью отказоустойчивого кластера Windows), можно настроить для экранированной виртуальной машины высокую доступность с помощью следующего командлета:

```powershell
Add-ClusterVirtualMachineRole -VMName 'MyShieldedVM' -Cluster <Hyper-V cluster name>
```

Экранированная виртуальная машина теперь может быть перенесена в кластер.

## <a name="next-step"></a>Далее

> [!div class="nextstepaction"]
> [Развертывание экранированного с помощью VMM](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)