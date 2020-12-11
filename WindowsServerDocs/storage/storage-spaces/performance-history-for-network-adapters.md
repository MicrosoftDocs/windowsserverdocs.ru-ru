---
description: Дополнительные сведения см. в статье журнал производительности для сетевых адаптеров.
title: Журнал производительности для сетевых адаптеров
ms.author: cosdar
manager: eldenc
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: c47b5f2ce60a952eb8c7773284d976e6b99d1477
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97040092"
---
# <a name="performance-history-for-network-adapters"></a>Журнал производительности для сетевых адаптеров

> Область применения: Windows Server 2019

Этот подраздел [журнала производительности для Локальные дисковые пространства](performance-history.md) подробно описывает журнал производительности, собранный для сетевых адаптеров. Журнал производительности сетевого адаптера доступен для каждого физического сетевого адаптера на каждом сервере в кластере. Журнал производительности удаленного доступа к памяти (RDMA) доступен для каждого физического сетевого адаптера с включенным RDMA.

   > [!NOTE]
   > Не удается собрать журнал производительности для сетевых адаптеров на недоступном сервере. Коллекция будет возобновлена автоматически при резервном копировании сервера.

## <a name="series-names-and-units"></a>Имена и единицы рядов

Эти серии собираются для каждого подходящего сетевого адаптера:

| Series                               | Единицы            |
|--------------------------------------|-----------------|
| `netadapter.bandwidth.inbound`       | бит в секунду |
| `netadapter.bandwidth.outbound`      | бит в секунду |
| `netadapter.bandwidth.total`         | бит в секунду |
| `netadapter.bandwidth.rdma.inbound`  | бит в секунду |
| `netadapter.bandwidth.rdma.outbound` | бит в секунду |
| `netadapter.bandwidth.rdma.total`    | бит в секунду |

   > [!NOTE]
   > Журнал производительности сетевого адаптера записывается в **битах** в секунду, а не в байтах в секунду. Сетевой адаптер 1 10 GbE может отправлять и принимать примерно 1 000 000 000 бит = 125 000 000 байт = 1,25 ГБ в секунду на теоретическом максимальном уровне.

## <a name="how-to-interpret"></a>Как интерпретировать

| Series                               | Как интерпретировать                                                      |
|--------------------------------------|-----------------------------------------------------------------------|
| `netadapter.bandwidth.inbound`       | Интенсивность получения данных сетевым адаптером.                         |
| `netadapter.bandwidth.outbound`      | Интенсивность передачи данных сетевым адаптером.                             |
| `netadapter.bandwidth.total`         | Общая скорость получения или отправки данных сетевым адаптером.           |
| `netadapter.bandwidth.rdma.inbound`  | Интенсивность получения данных через RDMA сетевым адаптером.               |
| `netadapter.bandwidth.rdma.outbound` | Интенсивность передачи данных через RDMA сетевым адаптером.                   |
| `netadapter.bandwidth.rdma.total`    | Общая скорость получения или отправки данных через RDMA сетевым адаптером. |

## <a name="where-they-come-from"></a>Откуда они приходят

`bytes.*`Ряды собираются из `Network Adapter` набора счетчиков производительности на сервере, где установлен сетевой адаптер, по одному экземпляру на сетевой адаптер.

| Series                           | Счетчик источника           |
|----------------------------------|--------------------------|
| `netadapter.bandwidth.inbound`   | 8 × `Bytes Received/sec` |
| `netadapter.bandwidth.outbound`  | 8 × `Bytes Sent/sec`     |
| `netadapter.bandwidth.total`     | 8 × `Bytes Total/sec`    |

`rdma.*`Ряды собираются из `RDMA Activity` набора счетчиков производительности на сервере, где установлен сетевой адаптер, по одному экземпляру на сетевой адаптер с включенным RDMA.

| Series                               | Счетчик источника           |
|--------------------------------------|--------------------------|
| `netadapter.bandwidth.rdma.inbound`  | 8 × `Inbound bytes/sec`  |
| `netadapter.bandwidth.rdma.outbound` | 8 × `Outbound bytes/sec` |
| `netadapter.bandwidth.rdma.total`    | 8 × *Сумма приведенного выше*   |

   > [!NOTE]
   > Счетчики измеряются для всего интервала, а не для выборки. Например, если сетевой адаптер бездействует 9 секунд, но передает 200 бит в десятую секунду, он `netadapter.bandwidth.total` будет записан в среднем 20 бит в секунду в течение этого 10-секундного интервала. Это гарантирует, что журнал производительности захватывает все действия и является надежным для шума.

## <a name="usage-in-powershell"></a>Использование в PowerShell

Используйте командлет [Get-NetAdapter](/powershell/module/netadapter/get-netadapter) :

```PowerShell
Get-NetAdapter <Name> | Get-ClusterPerf
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Журнал производительности для Локальных дисковых пространств](performance-history.md)
