---
title: Задать verbose
description: Справочная статья по параметру SET Verbose, которая указывает, следует ли предоставлять подробный вывод при создании теневой копии.
ms.topic: reference
ms.assetid: 93cb93c9-666f-4c74-814b-1c404a949935
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f0b1bbc08cffac858cdb26d69984d66e80531fe1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637642"
---
# <a name="set-verbose"></a>Задать verbose

Указывает, следует ли предоставлять подробный вывод при создании теневой копии. Если используется без параметров, команда **Set verbose** выводит справку из командной строки.

## <a name="syntax"></a>Синтаксис

```
set verbose {on | off}
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|-----------|-------------|
|    {on    |    off}     |

## <a name="remarks"></a>Примечания

-   Если параметр verbose имеет значение ON, **параметр SET** предоставляет сведения о включении или исключении модуля записи, а также сведения о сжатии и извлечении метаданных.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)