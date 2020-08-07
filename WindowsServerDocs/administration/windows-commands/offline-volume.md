---
title: offline volume
description: Справочная статья по команде "автономный том", которая принимает оперативный том с фокусом на состояние "вне сети".
ms.topic: article
ms.assetid: b8f7192f-ea38-47d0-9d4e-58ef68336ae6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e8a6bbebb88f97c4e4b04afccedeb05c4a1392a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885268"
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
