---
title: Журнал производительности для кластеров
ms.author: cosdar
manager: eldenc
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: ea80be97e3940850f9892c50c534c3449fd3ecdb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954671"
---
# <a name="performance-history-for-clusters"></a>Журнал производительности для кластеров

> Область применения: Windows Server 2019

Этот подраздел [журнала производительности для Локальные дисковые пространства](performance-history.md) описывает журнал производительности, собранный для кластеров.

Нет рядов, исходящих на уровне кластера. Вместо этого ряды серверов, такие как `clusternode.cpu.usage` , объединяются для всех серверов в кластере. Ряды томов, такие как `volume.iops.total` , объединяются для всех томов в кластере. И ряды дисков, такие как `physicaldisk.size.total` , объединяются для всех дисков в кластере.

## <a name="usage-in-powershell"></a>Использование в PowerShell

Используйте командлет [Get-Cluster](/powershell/module/failoverclusters/get-cluster) :

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Журнал производительности для Локальных дисковых пространств](performance-history.md)
