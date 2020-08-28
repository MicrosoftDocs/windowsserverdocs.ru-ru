---
title: bitsadmin cache и setlimit
description: Справочная статья по битсадмин кэшу и команде сетлимит, которая устанавливает предельный размер кэша.
ms.topic: reference
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: edcd83ace72e301471b03ac0c1fc85439a1c4d94
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028792"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin cache и setlimit

Задает предельный размер кэша.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /cache /setlimit percent
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| percent | Предельный размер кэша, определенный в процентах от общего пространства на жестком диске. |

## <a name="examples"></a>Примеры

Чтобы установить предельный размер кэша 50%:

```
bitsadmin /cache /setlimit 50
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда кэша битсадмин](bitsadmin-cache.md)
