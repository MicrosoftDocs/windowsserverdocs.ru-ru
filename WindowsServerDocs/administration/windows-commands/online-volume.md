---
title: online volume
description: Справочная статья по команде "оперативный том", которая принимает автономный том в состояние "в сети".
ms.topic: reference
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8847f340ebe3e295946550c46fd86bd59de300af
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89032692"
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
