---
title: bitsadmin util и version
description: Справочная статья по команде битсадмин util and Version, которая отображает версию службы BITS.
ms.topic: reference
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e28f179e48f837edbd4bc620b0a001b15289bd67
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820548"
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

| Параметр | Описание |
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
