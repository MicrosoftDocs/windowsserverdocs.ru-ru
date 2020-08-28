---
title: select
description: Справочная статья для * * * *-
ms.topic: reference
ms.assetid: 9eeb40c0-4258-46e2-8dbc-94f63497e771
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fb6230c24f723e20b09449967b157dd86347202
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89032226"
---
# <a name="select"></a>select



Перемещает фокус на диск, раздел, том или виртуальный жесткий диск (VHD).

## <a name="syntax"></a>Синтаксис

```
select disk
select partition
select volume
select vdisk
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|[Выбор диска](select-disk.md)|Перемещает фокус на диск.|
|[Выбор Секции](select-partition.md)|Сдвигает фокус на секцию.|
|[Выбор тома](select-volume.md)|Перемещает фокус на том.|
|[Выбрать виртуальный диск](select-vdisk.md)|Перемещает фокус на виртуальный жесткий диск.|

## <a name="remarks"></a>Remarks

-   Если выбран том с соответствующим разделом, раздел будет выбран автоматически.
-   Если секция выбрана с соответствующим томом, том будет выбран автоматически.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

