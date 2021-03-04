---
title: bitsadmin setmaxdownloadtime
description: Справочная статья по команде битсадмин сетмаксдовнлоадтиме, которая задает время ожидания загрузки в секундах.
ms.topic: reference
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9de5498416bdb24c0c2282ad26997ccfc3120aa0
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820898"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>bitsadmin setmaxdownloadtime

Задает время ожидания загрузки в секундах.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setmaxdownloadtime <job> <timeout>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| timeout | Длина времени ожидания скачивания в секундах. |

## <a name="examples"></a>Примеры

Чтобы задать время ожидания для задания с именем *мидовнлоаджоб* , равное 10 секундам.

```
bitsadmin /setmaxdownloadtime myDownloadJob 10
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
