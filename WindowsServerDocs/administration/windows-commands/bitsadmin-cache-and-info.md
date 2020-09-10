---
title: bitsadmin cache и info
description: Справочная статья по команде кэша битсадмин и info, которая создает дамп определенной записи кэша.
ms.topic: reference
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 16eda9ddd04a270fbfd754186fd5c9f4a6152cd5
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632555"
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
