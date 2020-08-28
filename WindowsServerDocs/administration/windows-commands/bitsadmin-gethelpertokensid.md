---
title: bitsadmin gethelpertokensid
description: Справочная статья по команде битсадмин жеселпертокенсид, которая возвращает идентификатор безопасности вспомогательного токена задания передачи BITS, если он задан.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 9cfa2c2a10d1f3947374262bbeb9ab21e559cfee
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033552"
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
