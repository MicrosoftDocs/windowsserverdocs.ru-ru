---
title: Расширение томов в локальных дисковых пространствах
description: Изменение размера томов в Локальные дисковые пространства с помощью Windows Admin Center и PowerShell.
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 05/07/2019
ms.openlocfilehash: 20482fe1728b12d4fe56dcfa397352fbb4b4f981
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366094"
---
# <a name="extending-volumes-in-storage-spaces-direct"></a>Расширение томов в локальных дисковых пространствах
> Относится к: Windows Server 2019, Windows Server 2016

В этом разделе приводятся инструкции по изменению размера томов в кластере [Локальные дисковые пространства](storage-spaces-direct-overview.md) с помощью центра администрирования Windows.

Ознакомьтесь с быстрым видео о том, как изменить размер тома.

> [!VIDEO https://www.youtube-nocookie.com/embed/hqyBzipBoTI]

## <a name="extending-volumes-using-windows-admin-center"></a>Расширение томов с помощью центра администрирования Windows

1. В центре администрирования Windows подключитесь к кластеру Локальные дисковые пространства, а затем выберите **тома** в области **инструменты** .
2. На странице тома выберите вкладку **Инвентаризация** , а затем выберите том, размер которого необходимо изменить.

    На странице сведения о томе указывается емкость хранилища для тома. Страницу сведений о томах также можно открыть непосредственно из панели мониторинга. На панели мониторинга на панели "оповещения" выберите оповещение, уведомляющее о нехватке объема хранилища для тома, а затем выберите команду **"переход к тому"** .

4. В верхней части страницы сведений о томах выберите **изменить размер**.
5. Введите новый больший размер, а затем выберите **изменить размер**.

    На странице сведения о томах отображается больший объем хранилища для тома, и оповещение на панели мониторинга удаляется.

## <a name="extending-volumes-using-powershell"></a>Расширение томов с помощью PowerShell

### <a name="capacity-in-the-storage-pool"></a>Емкость в пуле носителей

Прежде чем изменять размер тома, убедитесь, что у вас достаточно емкости в пуле носителей. Например, если размер тома с трехсторонним зеркальным отображением, который составляет 1 ТБ, меняется на 2 ТБ, занимаемое этим томом место увеличится с 3 до 6 ТБ. Для изменения размера необходимо по крайней мере 3 ТБ доступного места в пуле носителей (6 – 3 = 3).

### <a name="familiarity-with-volumes-in-storage-spaces"></a>Знакомство с томами в дисковых пространствах

В локальных дисковых пространствах каждый том состоит из нескольких объектов в стеке: общего тома кластера (CSV), т. е. тома; раздела; диска, т. е. виртуального диска; одного или нескольких уровней хранилища (если применимо). Чтобы изменить размер тома, необходимо изменить размер нескольких из этих объектов.

![volumes-in-smapi](media/resize-volumes/volumes-in-smapi.png)

Чтобы ознакомиться с ними, выполните командлет **Get-** с соответствующим существительным в PowerShell.

Пример:

```PowerShell
Get-VirtualDisk
```

Чтобы проследить связи между объектами в стеке, передайте один командлет **Get-** в следующий.

Например, вот как перейти от виртуального диска к его тому:

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-Disk | Get-Partition | Get-Volume 
```

### <a name="step-1--resize-the-virtual-disk"></a>Шаг 1. Изменение размера виртуального диска

В зависимости от способа создания, у виртуального диска могут быть уровни хранилища.

Чтобы проверить, выполните следующий командлет:

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier 
```

Если командлет ничего не возвращает, у виртуального диска нет уровней хранилища.

#### <a name="no-storage-tiers"></a>Нет уровней хранилища

Если у виртуального диска нет уровней хранилища, вы можете изменить его размер непосредственно с помощью командлета **Resize-VirtualDisk**.

Укажите новый размер в параметре **-Size**.

```PowerShell
Get-VirtualDisk <FriendlyName> | Resize-VirtualDisk -Size <Size>
```

При изменении размера **VirtualDisk** также автоматически изменяется размер **Disk**.

![Resize-VirtualDisk](media/resize-volumes/Resize-VirtualDisk.gif)

#### <a name="with-storage-tiers"></a>С уровнями хранилища

Если у виртуального диска есть уровни хранилища, вы можете изменить размер каждого уровня по отдельности с помощью командлета **Resize-StorageTier**.

Получите имена уровней хранилища, проследив связи с виртуального диска.

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier | Select FriendlyName
```

Затем укажите новый размер для каждого уровня в параметре **-Size**.

```PowerShell
Get-StorageTier <FriendlyName> | Resize-StorageTier -Size <Size>
```

> [!TIP]
> Если уровни отличаются по типу физического носителя (например, **MediaType = SSD** и **MediaType = HDD**), убедитесь, что в пуле носителей достаточно емкости каждого типа носителя.

При изменении размера **StorageTier** также автоматически изменяются размеры **VirtualDisk** и **Disk**.

![Resize-StorageTier](media/resize-volumes/Resize-StorageTier.gif)

### <a name="step-2--resize-the-partition"></a>Шаг 2. Изменение размера раздела

Измените размер раздела с помощью командлета **Resize-Partition**. Ожидается, что виртуальный диск содержит два раздела. Один из них зарезервирован и не должен меняться. Вам нужно изменить размер раздела **PartitionNumber = 2** и **Type = Basic**.

Укажите новый размер в параметре **-Size**. Рекомендуем использовать максимальный поддерживаемый размер, указанный ниже.

```PowerShell
# Choose virtual disk
$VirtualDisk = Get-VirtualDisk <FriendlyName>

# Get its partition
$Partition = $VirtualDisk | Get-Disk | Get-Partition | Where PartitionNumber -Eq 2

# Resize to its maximum supported size 
$Partition | Resize-Partition -Size ($Partition | Get-PartitionSupportedSize).SizeMax
```

При изменении размера **Partition** также автоматически изменяются размеры **Volume** и **ClusterSharedVolume**.

![Resize-Partition](media/resize-volumes/Resize-Partition.gif)

Вот и все!

> [!TIP]
> Чтобы убедиться, что размер тома изменился, выполните командлет **Get-Volume**.

## <a name="see-also"></a>См. также

- [Локальные дисковые пространства в Windows Server 2016](storage-spaces-direct-overview.md)
- [Планирование томов в Локальные дисковые пространства](plan-volumes.md)
- [Создание томов в Локальные дисковые пространства](create-volumes.md)
- [Удаление томов в Локальные дисковые пространства](delete-volumes.md)
