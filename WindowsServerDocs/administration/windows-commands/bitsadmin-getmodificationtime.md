---
title: bitsadmin getmodificationtime
description: Справочная статья по команде битсадмин жетмодификатионтиме, которая получает время последнего изменения задания или передачи данных.
ms.topic: reference
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f453d000d7f4085499306e9faf0ebc67b09deb1e
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821968"
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
