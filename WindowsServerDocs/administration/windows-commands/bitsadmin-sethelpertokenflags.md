---
title: bitsadmin sethelpertokenflags
description: Справочная статья по команде битсадмин сеселпертокенфлагс, которая устанавливает флаги использования вспомогательного токена, связанного с заданием передачи BITS.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 9cb562debae43be41ba1c126b0270ffbcf1e4f25
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028522"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

Задает флаги использования для [вспомогательного токена](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)   , связанного с заданием передачи BITS.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 3,0 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /sethelpertokenflags <job> <flags>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| flags | Возможные значения вспомогательных маркеров, включая:<ul><li>**0x0001.** Используется для открытия локального файла задания отправки, для создания или переименования временного файла задания загрузки, а также для создания или переименования файла ответов для задания отправки и ответа.</li><li>**0x0002.** Используется для открытия удаленного файла задания передачи или загрузки SMB, а также в ответ на HTTP-сервер или запрос прокси-сервера для неявных учетных данных NTLM или Kerberos.</li></ul>Необходимо вызвать,  `/setcredentialsjob targetscheme null null`   чтобы отправить учетные данные по протоколу HTTP. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
