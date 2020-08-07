---
title: ktmutil
description: Справочная статья по команде ктмутил, запускающей служебную программу диспетчера транзакций ядра.
ms.topic: article
ms.assetid: 53bc56df-f0e5-443b-ab20-bbf8b11d4a9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff65e7e228f4876e51e3132d3a430ceec3837053
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887663"
---
# <a name="ktmutil"></a>ktmutil

Запускает служебную программу диспетчера транзакций ядра. Если используется без параметров, **ктмутил** отображает доступные подкоманды.

## <a name="syntax"></a>Синтаксис

```
ktmutil list tms
ktmutil list transactions [{TmGUID}]
ktmutil resolve complete {TmGUID} {RmGUID} {EnGUID}
ktmutil resolve commit {TxGUID}
ktmutil resolve rollback {TxGUID}
ktmutil force commit {GUID}
ktmutil force rollback {GUID}
ktmutil forget
```

## <a name="examples"></a>Примеры


Чтобы принудительно зафиксировать незавершенные транзакции с идентификатором GUID 311a9209-03f4-11dc-918f-00188b8f707b, введите:

```
ktmutil force commit {311a9209-03f4-11dc-918f-00188b8f707b}
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)