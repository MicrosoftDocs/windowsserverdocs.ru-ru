---
title: bitsadmin getmodificationtime
description: Справочная статья по команде битсадмин жетмодификатионтиме, которая получает время последнего изменения задания или передачи данных.
ms.topic: reference
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 293b8ef47374c0df3f9b1cd3d76802d592c3c522
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631937"
---
# <a name="bitsadmin-getmodificationtime"></a>bitsadmin getmodificationtime

Извлекает время последнего изменения задания или передачи данных.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getmodificationtime <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить время последнего изменения для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getmodificationtime myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
