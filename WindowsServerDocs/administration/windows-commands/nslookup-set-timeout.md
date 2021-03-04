---
title: nslookup set timeout
description: Справочная статья по команде nslookup set timeout, которая изменяет начальное число секунд ожидания ответа на запрос поиска.
ms.topic: reference
ms.assetid: 07afdaf4-ffec-496f-a188-4e91cf1a28f8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4ac3a8e4aa9aabbe32fcefa9b1a1d2331e162f8d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101809629"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет начальное число секунд ожидания ответа на запрос поиска. Если ответ не получен в течение указанного промежутка времени, интервал времени ожидания удваивается, и запрос отсылается повторно. Используйте команду [nslookup set retry](nslookup-set-retry.md) , чтобы определить количество попыток отправки запроса.

## <a name="syntax"></a>Синтаксис

```
set timeout=<number>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| ---------- | ---------- |
| `<number>` | Указывает количество секунд ожидания ответа. Значение по умолчанию (в секундах) ожидания равно **5**. |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

Установка времени ожидания получения ответа в течение 2 секунд:

```
set timeout=2
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup set retry](nslookup-set-retry.md)
