---
title: bitsadmin cache и delete
description: Справочная статья по команде битсадмин Cache и DELETE, которая удаляет определенную запись кэша.
ms.topic: reference
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f56c100c8edfbb9c6bf782ffa71f20ef0cf0f338
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822598"
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
