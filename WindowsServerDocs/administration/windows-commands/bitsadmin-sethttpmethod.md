---
title: bitsadmin sethttpmethod
description: Справочная статья по команде битсадмин сесттпмесод, которая задает используемый HTTP-команду.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 8374a8e306f88cbdbad079d99233171712cc00bc
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026272"
---
# <a name="bitsadmin-sethttpmethod"></a>bitsadmin sethttpmethod

Задает используемую команду HTTP.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /sethttpmethod <job> <httpmethod>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| HttpMethod | Команда HTTP для использования. Дополнительные сведения о доступных командах см. в разделе [определения методов](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html). |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
