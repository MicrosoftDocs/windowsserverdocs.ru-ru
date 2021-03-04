---
title: bitsadmin getcompletiontime
description: Справочная статья по команде битсадмин жеткомплетионтиме, которая получает время завершения передачи данных заданием.
ms.topic: reference
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 72ab8bc41c0c6a185f7b31fba5448e335cd90518
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822238"
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
