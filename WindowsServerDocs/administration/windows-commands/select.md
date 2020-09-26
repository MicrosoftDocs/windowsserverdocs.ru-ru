---
title: выбор команд
description: Справочная статья по командам SELECT, которая перемещает фокус на диск, раздел, том или виртуальный жесткий диск (VHD).
ms.topic: reference
ms.assetid: 9eeb40c0-4258-46e2-8dbc-94f63497e771
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2b322fc7bf9355e64fbe14a0823c85dddadd6171
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389182"
---
# <a name="select-commands"></a>выбор команд

Перемещает фокус на диск, раздел, том или виртуальный жесткий диск (VHD).

## <a name="syntax"></a>Синтаксис

```
select disk
select partition
select vdisk
select volume
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| [Выбор диска](select-disk.md) | Перемещает фокус на диск. |
| [Выбор Секции](select-partition.md) | Сдвигает фокус на секцию. |
| [Выбрать виртуальный диск](select-vdisk.md) | Перемещает фокус на виртуальный жесткий диск. |
| [Выбор тома](select-volume.md) | Перемещает фокус на том. |

#### <a name="remarks"></a>Комментарии

- Если выбран том с соответствующим разделом, раздел будет выбран автоматически.

- Если секция выбрана с соответствующим томом, том будет выбран автоматически.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
