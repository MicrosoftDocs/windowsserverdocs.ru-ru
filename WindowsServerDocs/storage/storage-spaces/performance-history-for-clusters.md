---
description: Дополнительные сведения см. в статье журнал производительности для кластеров.
title: Журнал производительности для кластеров
ms.author: cosdar
manager: eldenc
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 14e2c493b4d93268d7d3e458c3cd3b2f53de1e1f
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97046172"
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
