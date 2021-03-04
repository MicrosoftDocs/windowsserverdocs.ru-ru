---
title: delete shadows
description: Справочная статья по команде delete Shadows, которая удаляет теневые копии.
ms.topic: reference
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: be88ca7d82ffb51ae814a02173412c1ca38d0fa2
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101819098"
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
