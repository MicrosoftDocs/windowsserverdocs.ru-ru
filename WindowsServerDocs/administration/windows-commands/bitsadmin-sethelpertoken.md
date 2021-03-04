---
title: bitsadmin sethelpertoken
description: Справочная статья по команде битсадмин сеселпертокен, которая задает основной маркер текущей командной строки (или маркер произвольной учетной записи локального пользователя, если он указан) в качестве вспомогательного токена задания передачи BITS.
ms.topic: reference
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 24421aac2f5ff8d24d7d593b4ff6d3f14cad07f8
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820988"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sethelpertoken

Задает основной маркер текущей командной строки (или маркер произвольной учетной записи локального пользователя, если он указан) в качестве [вспомогательного токена](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)задания передачи BITS.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 3,0 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /sethelpertoken <job> [<user_name@domain> <password>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| `<username@domain>` `<password>` | Необязательный параметр. Учетные данные локального пользователя, для которых используется токен. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
