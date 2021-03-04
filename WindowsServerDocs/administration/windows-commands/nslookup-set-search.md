---
title: nslookup set search
description: Справочная статья по команде nslookup set Search, которая добавляет имена доменов службы доменных имен (DNS) в список поиска доменов DNS для запроса, пока не будет получен ответ.
ms.topic: reference
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a3de4abb9b6ea00694605b8237ea43497b92dce8
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101809720"
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
| search | Добавляет доменные имена системы доменных имен (DNS) в список поиска доменов DNS для запроса, пока не будет получен ответ. Это значение по умолчанию. |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
