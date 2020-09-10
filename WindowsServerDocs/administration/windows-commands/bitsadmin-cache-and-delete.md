---
title: bitsadmin cache и delete
description: Справочная статья по команде битсадмин Cache и DELETE, которая удаляет определенную запись кэша.
ms.topic: reference
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3dd83b05b0b4964fe8dbaa52a03a651153d9a94d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632646"
---
# <a name="bitsadmin-cache-and-delete"></a>bitsadmin cache и delete

Удаляет определенную запись кэша.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /cache /delete recordID
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| recordID | Идентификатор GUID, связанный с записью кэша. |

## <a name="examples"></a>Примеры

Чтобы удалить запись кэша с RecordID {6511FB02-E195-40A2-B595-E8E2F8F47702}, сделайте следующее:

```
bitsadmin /cache /delete {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда кэша битсадмин](bitsadmin-cache.md)
