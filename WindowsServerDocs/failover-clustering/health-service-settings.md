---
description: 'Дополнительные сведения: параметры служба работоспособности'
title: Параметры служба работоспособности
manager: eldenc
ms.author: cosdar
ms.topic: article
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 7638b501e31985020c0bc32cbf47dd745c45db0f
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97047752"
---
# <a name="health-service-settings"></a>Параметры служба работоспособности

> Применяется к: Windows Server 2019, Windows Server 2016

Служба работоспособности — это новая функция Windows Server 2016, которая улучшает повседневный мониторинг и рабочую среду для кластеров под управлением Локальные дисковые пространства.

Многие параметры, управляющие поведением служба работоспособности, предоставляются в качестве параметров. Их можно изменить, чтобы настроить интенсивность ошибок или действий, включить или выключить определенное поведение и многое другое.

Используйте следующий командлет PowerShell, чтобы задать или изменить параметры.

### <a name="usage"></a>Использование

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name <SettingName> -Value <Value>
```

#### <a name="example"></a>Пример

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.Volume.CapacityThreshold.Warning" -Value 70
```

### <a name="common-settings"></a>Общие параметры

Ниже перечислены некоторые часто изменяемые параметры вместе со значениями по умолчанию.

#### <a name="volume-capacity-threshold"></a>Пороговое значение емкости тома

```
"System.Storage.Volume.CapacityThreshold.Enabled"  = True
"System.Storage.Volume.CapacityThreshold.Warning"  = 80
"System.Storage.Volume.CapacityThreshold.Critical" = 90
```

#### <a name="pool-reserve-capacity-threshold"></a>Порог резервирования емкости пула

```
"System.Storage.StoragePool.CheckPoolReserveCapacity.Enabled" = True
```

#### <a name="physical-disk-lifecycle"></a>Жизненный цикл физического диска

```
"System.Storage.PhysicalDisk.AutoPool.Enabled"                             = True
"System.Storage.PhysicalDisk.AutoRetire.OnLostCommunication.Enabled"       = True
"System.Storage.PhysicalDisk.AutoRetire.OnUnresponsive.Enabled"            = True
"System.Storage.PhysicalDisk.AutoRetire.DelayMs"                           = 900000 (i.e. 15 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountResetIntervalSeconds" = 360 (i.e. 60 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountAllowed"              = 3
```

#### <a name="supported-components-document"></a>Документ о поддерживаемых компонентах

См. предыдущий раздел.

#### <a name="firmware-rollout"></a>Развертывание встроенного по

```
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.SingleDrive.Enabled"       = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.Enabled"           = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelaySeconds"  = 604800 (i.e. 7 days)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.ShortDelaySeconds" = 86400 (i.e. 1 day)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelayCount"    = 1
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.FailureTolerance"  = 3
```

#### <a name="platform--quiescence"></a>Платформа или замороженной

```
"Platform.Quiescence.MinDelaySeconds" = 120 (i.e. 2 minutes)
"Platform.Quiescence.MaxDelaySeconds" = 420 (i.e. 7 minutes)
```

#### <a name="metrics"></a>Метрики

```
"System.Reports.ReportingPeriodSeconds" = 1
```

#### <a name="debugging"></a>Отладка

```
"System.LogLevel" = 4
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Служба работоспособности в Windows Server 2016](health-service-overview.md)
- [Локальные дисковые пространства в Windows Server 2016](../storage/storage-spaces/storage-spaces-direct-overview.md)
