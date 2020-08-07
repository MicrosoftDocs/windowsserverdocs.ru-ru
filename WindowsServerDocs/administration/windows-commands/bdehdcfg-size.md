---
title: bdehdcfg size
description: Справочная статья по команде размера BdeHdCfg, которая указывает размер системного раздела при создании нового системного диска.
ms.topic: article
ms.assetid: 80f55b1d-a28d-4edf-9997-1fb918b7b5a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc511f72e721561ce27e20b55ceda2e10bb0fdf4
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895073"
---
# <a name="bdehdcfg-size"></a>BdeHdCfg: размер

Указывает размер системного раздела при создании нового системного диска. Если размер не указан, средство будет использовать значение по умолчанию 300 МБ. Минимальный размер системного диска составляет 100 МБ. Если вы будете хранить в системном разделе Восстановление системы или другие системные средства, следует соответственно увеличить размер.

> [!NOTE]
> Команда **size** не может быть объединена с `target <drive_letter> merge` командой.

## <a name="syntax"></a>Синтаксис

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink} -size <size_in_mb>
```

#### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<size_in_mb>` | Указывает количество мегабайтов (МБ), используемых для новой секции. |

## <a name="examples"></a>Примеры

Чтобы выделить 500 МБ на системный диск по умолчанию:

```
bdehdcfg -target default -size 500
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
