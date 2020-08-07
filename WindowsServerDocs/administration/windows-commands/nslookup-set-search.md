---
title: nslookup set search
description: Справочная статья по команде nslookup set Search, которая добавляет имена доменов службы доменных имен (DNS) в список поиска доменов DNS для запроса, пока не будет получен ответ.
ms.topic: article
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91592daf702741fafcb88de792836f5183868101
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885540"
---
# <a name="nslookup-set-search"></a>nslookup set search

Добавляет доменные имена DNS в списке поиска доменов DNS в запрос, пока не будет получен ответ. Это применимо, когда набор и запрос уточняющего запроса содержат по крайней мере одну точку, но не заканчиваются точкой в конце.

## <a name="syntax"></a>Синтаксис

```
set [no]search
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| не искать | Прекращает добавление доменных имен службы доменных имен (DNS) в списке поиска доменов DNS для запроса. |
| search | Добавляет доменные имена системы доменных имен (DNS) в список поиска доменов DNS для запроса, пока не будет получен ответ. Это значение по умолчанию. |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
