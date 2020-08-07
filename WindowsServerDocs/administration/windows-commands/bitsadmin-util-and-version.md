---
title: bitsadmin util и version
description: Справочная статья по команде битсадмин util and Version, которая отображает версию службы BITS.
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c3490fe4e3eaa217b81287d8a2ed38a6fdb98279
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880796"
---
# <a name="bitsadmin-util-and-version"></a>bitsadmin util и version

Отображает версию службы BITS (например, 2,0).

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 1,5 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /util /version [/verbose]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| /verbose | Используйте этот параметр, чтобы отобразить версию файла для каждой библиотеки DLL, связанной с BITS, и проверить, может ли запускаться служба BITS.|

## <a name="examples"></a>Примеры

Для вывода версии службы BITS.

```
bitsadmin /util /version
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [битсадмин util, команда](bitsadmin-util.md)

- [Команда битсадмин](bitsadmin.md)
