---
title: bitsadmin gethelpertokenflags
description: Справочная статья по команде битсадмин жеселпертокенфлагс, которая возвращает флаги использования вспомогательного токена, связанного с заданием передачи BITS.
ms.topic: reference
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 4a7a203046ef3d74c311a50a7b082394c2ca28c9
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821998"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitsadmin gethelpertokenflags

Возвращает флаги использования для [вспомогательного токена](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs) , связанного с заданием передачи BITS.

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

### <a name="remarks"></a>Комментарии

Возможные возвращаемые значения, включая:

- **0x0001.** Вспомогательный токен используется для открытия локального файла задания отправки, создания или переименования временного файла задания загрузки, а также для создания или переименования файла ответов для задания отправки и ответа.

- **0x0002.** Вспомогательный токен используется для открытия удаленного файла задания передачи или загрузки SMB, а также в ответ на HTTP-сервер или запрос прокси-сервера для неявных учетных данных NTLM или Kerberos. Необходимо вызвать, `/SetCredentialsJob TargetScheme NULL NULL` чтобы разрешить отправку учетных данных по протоколу HTTP.

## <a name="examples"></a>Примеры

Чтобы получить флаги использования для вспомогательного токена, связанного с заданием передачи BITS с именем *мидовнлоаджоб*:

```
bitsadmin /gethelpertokenflags myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
