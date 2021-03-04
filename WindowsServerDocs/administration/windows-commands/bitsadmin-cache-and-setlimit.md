---
title: bitsadmin cache и setlimit
description: Справочная статья по битсадмин кэшу и команде сетлимит, которая устанавливает предельный размер кэша.
ms.topic: reference
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7ee5e86749421b11cd4087afdbdc3abb4f4e86c3
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822428"
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
