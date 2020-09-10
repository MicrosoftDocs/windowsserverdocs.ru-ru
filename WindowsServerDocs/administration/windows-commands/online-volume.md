---
title: online volume
description: Справочная статья по команде "оперативный том", которая принимает автономный том в состояние "в сети".
ms.topic: reference
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a53b3e3955f1435c9f34b4d2b16f17685d6b3bb4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627278"
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
