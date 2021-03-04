---
title: bitsadmin sethttpmethod
description: Справочная статья по команде битсадмин сесттпмесод, которая задает используемый HTTP-команду.
ms.topic: reference
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 547f800c33f6d3fca63c2ec03efee051848e2333
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820968"
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
