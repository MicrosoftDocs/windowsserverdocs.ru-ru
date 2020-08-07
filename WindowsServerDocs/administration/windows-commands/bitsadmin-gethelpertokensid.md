---
title: bitsadmin gethelpertokensid
description: Справочная статья по команде битсадмин жеселпертокенсид, которая возвращает идентификатор безопасности вспомогательного токена задания передачи BITS, если он задан.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 742c009d1625fe5ba755367a2a93310627d10550
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894232"
---
# <a name="bitsadmin-gethelpertokensid"></a>bitsadmin gethelpertokensid

Возвращает идентификатор безопасности [вспомогательного токена](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)задания передачи BITS, если он задан.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 3,0 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /gethelpertokensid <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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
