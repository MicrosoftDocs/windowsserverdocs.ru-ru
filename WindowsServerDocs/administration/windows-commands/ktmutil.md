---
title: ktmutil
description: Справочная статья по команде ктмутил, запускающей служебную программу диспетчера транзакций ядра.
ms.topic: reference
ms.assetid: 53bc56df-f0e5-443b-ab20-bbf8b11d4a9a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 07067415406a0f8ba88d24362ec1b6252f8b88cc
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627590"
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