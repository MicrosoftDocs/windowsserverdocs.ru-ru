---
title: delete shadows
description: Справочная статья по команде delete Shadows, которая удаляет теневые копии.
ms.topic: reference
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d2613fc978db8c8e5b323df142b204a7270f6bad
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024208"
---
# <a name="delete-shadows"></a>delete shadows

Удаляет теневые копии.

## <a name="syntax"></a>Синтаксис

```
delete shadows [all | volume <volume> | oldest <volume> | set <setID> | id <shadowID> | exposed {<drive> | <mountpoint>}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| ---- | ---- |
| все | Удаляет все теневые копии. |
| тома `<volume>` | Удаляет все теневые копии данного тома. |
| Ранняя `<volume>` | Удаляет самую старую теневую копию заданного тома. |
| параметр `<setID>` | Удаляет теневые копии в наборе теневых копий заданного идентификатора. Псевдоним можно указать с помощью **%** символа, если он существует в текущей среде. |
| удостоверения `<shadowID>` | Удаляет теневую копию заданного идентификатора. Псевдоним можно указать с помощью **%** символа, если он существует в текущей среде. |
| предоставлено {'<drive> | <mountpoint>} |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [удалить команду](delete.md)
