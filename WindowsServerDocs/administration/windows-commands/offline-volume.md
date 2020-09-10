---
title: offline volume
description: Справочная статья по команде "автономный том", которая принимает оперативный том с фокусом на состояние "вне сети".
ms.topic: reference
ms.assetid: b8f7192f-ea38-47d0-9d4e-58ef68336ae6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7902ef109c7e893d2610ae308a391d9efafbabfd
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627373"
---
# <a name="offline-volume"></a>offline volume

Перевод сетевого тома в состояние "вне сети".

> [!NOTE]
> Для завершения команды " **автономный том** " необходимо выбрать том. Используйте команду [Выбор тома](select-volume.md) , чтобы выбрать диск и переместить фокус на него.

## <a name="syntax"></a>Синтаксис

```
offline volume [noerr]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| Noerr | Только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

### <a name="examples"></a>Примеры

Чтобы перевести диск с фокусом в режим вне сети, введите:

```
offline volume
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
