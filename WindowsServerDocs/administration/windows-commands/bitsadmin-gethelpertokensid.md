---
title: bitsadmin gethelpertokensid
description: Справочная статья по команде битсадмин жеселпертокенсид, которая возвращает идентификатор безопасности вспомогательного токена задания передачи BITS, если он задан.
ms.topic: reference
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: b97409f98eba6df61ecf678edc6c1b6e30e47370
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822028"
---
# <a name="bitsadmin-gethelpertokensid"></a>bitsadmin gethelpertokensid

Возвращает идентификатор безопасности [вспомогательного токена](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)задания передачи BITS, если он задан.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 3,0 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /gethelpertokensid <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить идентификатор безопасности для задания передачи BITS с именем *мидовнлоаджоб*, сделайте следующее:

```
bitsadmin /gethelpertokensid myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
