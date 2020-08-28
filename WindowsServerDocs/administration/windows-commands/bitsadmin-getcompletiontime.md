---
title: bitsadmin getcompletiontime
description: Справочная статья по команде битсадмин жеткомплетионтиме, которая получает время завершения передачи данных заданием.
ms.topic: reference
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d79fbf49aa4ec9cea60829a3b0859887da0e5dd5
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033682"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime

Возвращает время, когда задание завершило передачу данных.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getcompletiontime <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить время, когда задание с именем *мидовнлоаджоб* завершило передачу данных, сделайте следующее:

```
bitsadmin /getcompletiontime myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
