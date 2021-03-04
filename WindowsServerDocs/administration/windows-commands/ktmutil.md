---
title: ktmutil
description: Справочная статья по команде ктмутил, запускающей служебную программу диспетчера транзакций ядра.
ms.topic: reference
ms.assetid: 53bc56df-f0e5-443b-ab20-bbf8b11d4a9a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 33978534b301f01e112e67928b5beaac153e3beb
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101814514"
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