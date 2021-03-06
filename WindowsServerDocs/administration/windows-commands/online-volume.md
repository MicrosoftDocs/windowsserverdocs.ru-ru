---
title: online volume
description: Справочная статья по команде "оперативный том", которая принимает автономный том в состояние "в сети".
ms.topic: reference
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f8aa460438e011b9b6f05af770af7a8aab500c70
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101809073"
---
# <a name="online-volume"></a>online volume

Переводит автономный том в состояние "в сети". Эта команда работает с томами, на которых произошел сбой, не выполняется или находится в состоянии сбоя избыточности.

> [!NOTE]
> Для завершения команды " **оперативный том** " необходимо выбрать том. Используйте команду [выбрать том](select-volume.md) , чтобы выбрать том и переместить фокус на него.

> [!IMPORTANT]
> Эта команда завершается ошибкой, если она используется на диске, доступном только для чтения.

## <a name="syntax"></a>Синтаксис

```
online volume [noerr]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| Noerr | Только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

### <a name="examples"></a>Примеры

Чтобы перевести том с фокусом в режим «в сети», введите:

```
online volume
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
