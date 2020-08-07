---
title: delete shadows
description: Справочная статья по команде delete Shadows, которая удаляет теневые копии.
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 29d1679b2d05265aa1fb5a089fab9cf99f840cd9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891378"
---
# <a name="delete-shadows"></a>delete shadows

Удаляет теневые копии.

## <a name="syntax"></a>Синтаксис

```
delete shadows [all | volume <volume> | oldest <volume> | set <setID> | id <shadowID> | exposed {<drive> | <mountpoint>}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| ---- | ---- |
| все | Удаляет все теневые копии. |
| тома`<volume>` | Удаляет все теневые копии данного тома. |
| Ранняя`<volume>` | Удаляет самую старую теневую копию заданного тома. |
| параметр`<setID>` | Удаляет теневые копии в наборе теневых копий заданного идентификатора. Псевдоним можно указать с помощью **%** символа, если он существует в текущей среде. |
| удостоверения`<shadowID>` | Удаляет теневую копию заданного идентификатора. Псевдоним можно указать с помощью **%** символа, если он существует в текущей среде. |
| предоставлено {'<drive> | <mountpoint>} |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [удалить команду](delete.md)
