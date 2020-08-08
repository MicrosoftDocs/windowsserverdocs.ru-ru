---
title: Журнал производительности для дисков
ms.author: cosdar
manager: eldenc
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4d344db75539e4455c11c02f336edc9275d3c813
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965971"
---
# <a name="performance-history-for-drives"></a>Журнал производительности для дисков

> Область применения: Windows Server 2019

В этом подразделе [журнала производительности для Локальные дисковые пространства](performance-history.md) подробно описывается журнал производительности, собранный для дисков. Журнал производительности доступен для каждого диска в подсистеме хранения кластера, независимо от шины или типа носителя. Однако он недоступен для загрузочных дисков операционной системы.

   > [!NOTE]
   > Не удается собрать журнал производительности для дисков на недоступном сервере. Коллекция будет возобновлена автоматически при резервном копировании сервера.

## <a name="series-names-and-units"></a>Имена и единицы рядов

Эти серии собираются для каждого подходящего диска:

| Series                          | Единица измерения             |
|---------------------------------|------------------|
| `physicaldisk.iops.read`        | в секунду       |
| `physicaldisk.iops.write`       | в секунду       |
| `physicaldisk.iops.total`       | в секунду       |
| `physicaldisk.throughput.read`  | байт в секунду |
| `physicaldisk.throughput.write` | байт в секунду |
| `physicaldisk.throughput.total` | байт в секунду |
| `physicaldisk.latency.read`     | секунд          |
| `physicaldisk.latency.write`    | секунд          |
| `physicaldisk.latency.average`  | секунд          |
| `physicaldisk.size.total`       | Байты            |
| `physicaldisk.size.used`        | Байты            |

## <a name="how-to-interpret"></a>Как интерпретировать

| Series                          | Как интерпретировать                                                            |
|---------------------------------|-----------------------------------------------------------------------------|
| `physicaldisk.iops.read`        | Число операций чтения в секунду, выполненных диском.                |
| `physicaldisk.iops.write`       | Число операций записи в секунду, выполненных диском.               |
| `physicaldisk.iops.total`       | Общее число операций чтения или записи в секунду, выполненных диском. |
| `physicaldisk.throughput.read`  | Количество данных, считанных с диска в секунду.                            |
| `physicaldisk.throughput.write` | Количество данных, записываемых на диск в секунду.                           |
| `physicaldisk.throughput.total` | Общее количество данных, считанных или записанных на диск в секунду.        |
| `physicaldisk.latency.read`     | Средняя задержка операций чтения с диска.                          |
| `physicaldisk.latency.write`    | Средняя задержка операций записи на диск.                           |
| `physicaldisk.latency.average`  | Средняя задержка всех операций на диск или с него.                     |
| `physicaldisk.size.total`       | Общий объем хранилища диска.                                    |
| `physicaldisk.size.used`        | Используемая емкость хранилища диска.                                     |

## <a name="where-they-come-from"></a>Откуда они приходят

`iops.*`Ряды, `throughput.*` и `latency.*` собираются из `Physical Disk` набора счетчиков производительности на сервере, подключенном к диску, по одному экземпляру на диск. Эти счетчики измеряются `partmgr.sys` и не включают большую часть стека программного обеспечения Windows и других прыжков сети. Они представляют собой представление о производительности оборудования устройства.

| Series                          | Счетчик источника           |
|---------------------------------|--------------------------|
| `physicaldisk.iops.read`        | `Disk Reads/sec`         |
| `physicaldisk.iops.write`       | `Disk Writes/sec`        |
| `physicaldisk.iops.total`       | `Disk Transfers/sec`     |
| `physicaldisk.throughput.read`  | `Disk Read Bytes/sec`    |
| `physicaldisk.throughput.write` | `Disk Write Bytes/sec`   |
| `physicaldisk.throughput.total` | `Disk Bytes/sec`         |
| `physicaldisk.latency.read`     | `Avg. Disk sec/Read`     |
| `physicaldisk.latency.write`    | `Avg. Disk sec/Writes`   |
| `physicaldisk.latency.average`  | `Avg. Disk sec/Transfer` |

   > [!NOTE]
   > Счетчики измеряются для всего интервала, а не для выборки. Например, если диск бездействует в течение 9 секунд, но завершает 30 IOs в десятой секунде, он `physicaldisk.iops.total` будет записан в среднем 3 iOS в секунду в течение этого 10-секундного интервала. Это гарантирует, что журнал производительности захватывает все действия и является надежным для шума.

`size.*`Ряды собираются из `MSFT_PhysicalDisk` класса в WMI, по одному экземпляру на диск.

| Series                          | Source, свойство        |
|---------------------------------|------------------------|
| `physicaldisk.size.total`       | `Size`                 |
| `physicaldisk.size.used`        | `VirtualDiskFootprint` |

## <a name="usage-in-powershell"></a>Использование в PowerShell

Используйте командлет [Get-физический](/powershell/module/storage/get-physicaldisk) :

```PowerShell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Get-ClusterPerf
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Журнал производительности для Локальных дисковых пространств](performance-history.md)
