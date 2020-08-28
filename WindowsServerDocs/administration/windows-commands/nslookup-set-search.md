---
title: nslookup set search
description: Справочная статья по команде nslookup set Search, которая добавляет имена доменов службы доменных имен (DNS) в список поиска доменов DNS для запроса, пока не будет получен ответ.
ms.topic: reference
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 17cee7cbc2112db346c91ab4a7b88264eff6a850
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025158"
---
# <a name="nslookup-set-search"></a>nslookup set search

Добавляет доменные имена DNS в списке поиска доменов DNS в запрос, пока не будет получен ответ. Это применимо, когда набор и запрос уточняющего запроса содержат по крайней мере одну точку, но не заканчиваются точкой в конце.

## <a name="syntax"></a>Синтаксис

```
set [no]search
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| не искать | Прекращает добавление доменных имен службы доменных имен (DNS) в списке поиска доменов DNS для запроса. |
| поиск | Добавляет доменные имена системы доменных имен (DNS) в список поиска доменов DNS для запроса, пока не будет получен ответ. Это значение по умолчанию. |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
