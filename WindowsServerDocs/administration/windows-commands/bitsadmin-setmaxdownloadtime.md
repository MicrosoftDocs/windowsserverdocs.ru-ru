---
title: bitsadmin setmaxdownloadtime
description: Справочная статья по команде битсадмин сетмаксдовнлоадтиме, которая задает время ожидания загрузки в секундах.
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5453c476f304bce3564167da93518793d7eef043
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893117"
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
