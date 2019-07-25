---
title: Развертывание графических устройств с помощью дискретного назначения устройств
description: Узнайте, как использовать ДДА для развертывания графических устройств в Windows Server
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 67a01889-fa36-4bc6-841d-363d76df6a66
ms.openlocfilehash: 2f9d283f5f80d6bb0851b2abd93be0f4c10899c8
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476589"
---
# <a name="deploy-graphics-devices-using-discrete-device-assignment"></a>Развертывание графических устройств с помощью дискретного назначения устройств

>Область применения. Microsoft Hyper-V Server 2016, Windows Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019  

Начиная с Windows Server 2016 можно использовать дискретное назначение устройств или ДДА для передачи целого устройства PCIe в виртуальную машину.  Это обеспечит высокопроизводительный доступ к устройствам, например к [хранилищу NVMe](./Deploying-storage-devices-using-dda.md) или графическим картам, из виртуальной машины, в то время как они смогут использовать собственные драйверы устройств.  Дополнительные сведения о том, какие устройства работают, каковы возможные последствия для безопасности и т. д., см. в [плане развертывания устройств с помощью дискретного назначения устройств](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) .

Использование устройства с дискретным назначением устройств состоит из трех этапов:
-   Настройка виртуальной машины для назначения дискретного устройства
-   Отключение устройства от раздела узла
-   Назначение устройства гостевой виртуальной машине

Все команды могут выполняться на узле в консоли Windows PowerShell с правами администратора.

## <a name="configure-the-vm-for-dda"></a>Настройка виртуальной машины для ДДА
Отдельное назначение устройств накладывает некоторые ограничения на виртуальные машины, и необходимо выполнить следующий шаг.

1.  Настройте параметр "Автоматическое действие при автоматическом запуске" для виртуальной машины в Турнофф, выполнив

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

### <a name="some-additional-vm-preparation-is-required-for-graphics-devices"></a>Для графических устройств требуется подготовка дополнительных виртуальных машин.

Некоторое оборудование работает лучше, если виртуальная машина настроена определенным образом.  Дополнительные сведения о том, требуются ли для оборудования следующие конфигурации, вы можете получить у поставщика оборудования. Дополнительные сведения можно найти в [плане по планированию развертывания устройств с помощью дискретного назначения устройств](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) и в этой [записи блога.](https://techcommunity.microsoft.com/t5/Virtualization/Discrete-Device-Assignment-GPUs/ba-p/382266)

1. Включение объединения с возможностью записи в ЦП
   ```
   Set-VM -GuestControlledCacheTypes $true -VMName VMName
   ```
2. Настройка 32-разрядного пространства MMIO
   ```
   Set-VM -LowMemoryMappedIoSpace 3Gb -VMName VMName
   ```
3. Настройка более 32-разрядного пространства MMIO
   ```
   Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName VMName
   ```
   > [!TIP] 
   > Приведенные выше значения пространства MMIO являются разумными значениями, которые можно задать для экспериментов с одним GPU.  Если после запуска виртуальной машины устройство сообщает об ошибке, связанной с недостаточным объемом ресурсов, скорее всего, потребуется изменить эти значения. Изучите [план развертывания устройств с помощью дискретного назначения устройств](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) , чтобы узнать, как точно рассчитать требования MMIO.

## <a name="dismount-the-device-from-the-host-partition"></a>Отключение устройства от раздела узла
### <a name="optional---install-the-partitioning-driver"></a>Необязательно. Установка драйвера секционирования
Отдельное назначение устройств предоставляет поставщикам оборудования возможность предоставлять драйвер защиты с помощью устройств.  Обратите внимание, что этот драйвер не совпадает с драйвером устройства, который будет установлен на гостевой виртуальной машине.  Однако необходимо, чтобы поставщик оборудования предоставил этот драйвер, но если он предоставил его, установите его перед отключением устройства от раздела узла.  Обратитесь к поставщику оборудования за дополнительными сведениями о том, есть ли у них драйвер по устранению рисков.
> Если драйвер секционирования не указан, во время отключения необходимо использовать `-force` параметр, чтобы обойти предупреждение системы безопасности. Дополнительные сведения о влиянии этого действия на вопросы безопасности см. в статье [Планирование развертывания устройств с помощью дискретного назначения устройств](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md).

### <a name="locating-the-devices-location-path"></a>Поиск пути к расположению устройства
Для отключения и подключения устройства к узлу требуется указать путь к расположению PCI.  Пример пути к расположению выглядит следующим образом: `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`.  Дополнительные сведения о расположении пути расположения можно найти здесь: [Планирование развертывания устройств с помощью дискретного назначения устройств](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md).

### <a name="disable-the-device"></a>Отключение устройства
С помощью Device Manager или PowerShell убедитесь, что устройство отключено.  

### <a name="dismount-the-device"></a>Отключение устройства
В зависимости от того, предоставил ли поставщик драйвер по устранению рисков, необходимо использовать параметр «-Force».
- Если установлен драйвер устранения рисков
  ```
  Dismount-VMHostAssignableDevice -LocationPath $locationPath
  ```
- Если драйвер устранения рисков не был установлен
  ```
  Dismount-VMHostAssignableDevice -force -LocationPath $locationPath
  ```

## <a name="assigning-the-device-to-the-guest-vm"></a>Назначение устройства гостевой виртуальной машине
Последний шаг — сообщить Hyper-V, что виртуальная машина должна иметь доступ к устройству.  Помимо пути к расположению, приведенному выше, необходимо знать имя виртуальной машины.

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>Что дальше
После успешной установки устройства в виртуальной машине теперь можно запустить эту виртуальную машину и взаимодействовать с устройством, как обычно при работе в системе без операционной системы.  Это означает, что теперь вы можете установить драйверы поставщика оборудования на виртуальной машине, и приложения смогут увидеть это оборудование.  Это можно проверить, открыв диспетчер устройств на гостевой виртуальной машине и просмотрев, что оборудование теперь отображается.

## <a name="removing-a-device-and-returning-it-to-the-host"></a>Удаление устройства и его возврат на узел
Если вы хотите вернуть устройство в исходное состояние, необходимо будет закрыть виртуальную машину и выдать следующее:
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
Затем можно снова включить устройство в диспетчере устройств, и операционная система узла сможет снова взаимодействовать с устройством.

## <a name="examples"></a>Примеры

### <a name="mounting-a-gpu-to-a-vm"></a>Подключение графического процессора к виртуальной машине
В этом примере мы используем PowerShell для настройки виртуальной машины с именем "ddatest1", чтобы взять первый GPU, доступный изготовителем NVIDIA, и назначить его виртуальной машине.  
```
#Configure the VM for a Discrete Device Assignment
$vm =   "ddatest1"
#Set automatic stop action to TurnOff
Set-VM -Name $vm -AutomaticStopAction TurnOff
#Enable Write-Combining on the CPU
Set-VM -GuestControlledCacheTypes $true -VMName $vm
#Configure 32 bit MMIO space
Set-VM -LowMemoryMappedIoSpace 3Gb -VMName $vm
#Configure Greater than 32 bit MMIO space
Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName $vm

#Find the Location Path and disable the Device
#Enumerate all PNP Devices on the system
$pnpdevs = Get-PnpDevice -presentOnly
#Select only those devices that are Display devices manufactured by NVIDIA
$gpudevs = $pnpdevs |where-object {$_.Class -like "Display" -and $_.Manufacturer -like "NVIDIA"}
#Select the location path of the first device that's available to be dismounted by the host.
$locationPath = ($gpudevs | Get-PnpDeviceProperty DEVPKEY_Device_LocationPaths).data[0]
#Disable the PNP Device
Disable-PnpDevice  -InstanceId $gpudevs[0].InstanceId

#Dismount the Device from the Host
Dismount-VMHostAssignableDevice -force -LocationPath $locationPath

#Assign the device to the guest VM.
Add-VMAssignableDevice -LocationPath $locationPath -VMName $vm
```
