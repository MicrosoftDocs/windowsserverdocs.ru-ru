---
title: bitsadmin sethelpertoken
description: Справочная статья по команде битсадмин сеселпертокен, которая задает основной маркер текущей командной строки (или маркер произвольной учетной записи локального пользователя, если он указан) в качестве вспомогательного токена задания передачи BITS.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: a691d010aa112f1ac609077be6a6968f79d73c72
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630915"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sethelpertoken

Задает основной маркер текущей командной строки (или маркер произвольной учетной записи локального пользователя, если он указан) в качестве [вспомогательного токена](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)задания передачи BITS.

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
