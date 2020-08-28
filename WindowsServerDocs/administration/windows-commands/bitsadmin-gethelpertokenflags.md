---
title: bitsadmin gethelpertokenflags
description: Справочная статья по команде битсадмин жеселпертокенфлагс, которая возвращает флаги использования вспомогательного токена, связанного с заданием передачи BITS.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 59c6f2913c3c0f9bde3bbd591cf4a887e50af801
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033562"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitsadmin gethelpertokenflags

Возвращает флаги использования для [вспомогательного токена](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)   , связанного с заданием передачи BITS.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 3,0 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /gethelpertokenflags <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

### <a name="remarks"></a>Remarks

Возможные возвращаемые значения, включая:

- **0x0001.** Вспомогательный токен используется для открытия локального файла задания отправки, создания или переименования временного файла задания загрузки, а также для создания или переименования файла ответов для задания отправки и ответа.

- **0x0002.** Вспомогательный токен используется для открытия удаленного файла задания передачи или загрузки SMB, а также в ответ на HTTP-сервер или запрос прокси-сервера для неявных учетных данных NTLM или Kerberos. Необходимо вызвать,  `/SetCredentialsJob TargetScheme NULL NULL`   чтобы разрешить отправку учетных данных по протоколу HTTP.

## <a name="examples"></a>Примеры

Чтобы получить флаги использования для вспомогательного токена, связанного с заданием передачи BITS с именем *мидовнлоаджоб*:

```
bitsadmin /gethelpertokenflags myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
