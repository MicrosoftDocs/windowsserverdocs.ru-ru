---
title: bitsadmin cache и delete
description: Справочная статья по команде битсадмин Cache и DELETE, которая удаляет определенную запись кэша.
ms.topic: reference
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b7a7c00013833df121219f3e4f17e55a1d1e7d4
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034902"
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
