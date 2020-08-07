---
title: bitsadmin cache и setlimit
description: Справочная статья по битсадмин кэшу и команде сетлимит, которая устанавливает предельный размер кэша.
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41a1331a19f66e7d84dc3eb57b04d42596a40628
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894703"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin cache и setlimit

Задает предельный размер кэша.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /cache /setlimit percent
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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
