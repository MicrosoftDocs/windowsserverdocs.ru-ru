---
title: bitsadmin sethttpmethod
description: Справочная статья по команде битсадмин сесттпмесод, которая задает используемый HTTP-команду.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 9b782ea4f07113541ce62eaef63ac8047141e766
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881041"
---
# <a name="bitsadmin-sethttpmethod"></a>bitsadmin sethttpmethod

Задает используемую команду HTTP.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /sethttpmethod <job> <httpmethod>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| HttpMethod | Команда HTTP для использования. Дополнительные сведения о доступных командах см. в разделе [определения методов](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html). |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
