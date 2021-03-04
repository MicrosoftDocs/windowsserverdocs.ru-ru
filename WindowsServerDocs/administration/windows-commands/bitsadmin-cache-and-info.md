---
title: bitsadmin cache и info
description: Справочная статья по команде кэша битсадмин и info, которая создает дамп определенной записи кэша.
ms.topic: reference
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bd3793c14239f8b6b8cb586ef71b0fb76a64a660
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822458"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin cache и info

Создает дамп определенной записи кэша.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /cache /info recordID [/verbose]
```

### <a name="parameters"></a>Параметры

| парамретер | Описание |
| -------------- | -------------- |
| recordID | Идентификатор GUID, связанный с записью кэша. |

## <a name="examples"></a>Примеры

Чтобы сохранить запись кэша с значением recordID, равным {6511FB02-E195-40A2-B595-E8E2F8F47702}:

```
bitsadmin /cache /info {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда кэша битсадмин](bitsadmin-cache.md)
