---
title: bitsadmin getmodificationtime
description: Справочная статья по команде битсадмин жетмодификатионтиме, которая получает время последнего изменения задания или передачи данных.
ms.topic: article
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d89d3382c738ffc473135579eb58590f06774d5c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894168"
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
