---
title: Задать verbose
description: Справочная статья по параметру SET Verbose, которая указывает, следует ли предоставлять подробный вывод при создании теневой копии.
ms.topic: reference
ms.assetid: 93cb93c9-666f-4c74-814b-1c404a949935
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 823c43e1ee6f42b36a922473b870c80d392e1f6c
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024908"
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

## <a name="remarks"></a>Remarks

-   Если параметр verbose имеет значение ON, **параметр SET** предоставляет сведения о включении или исключении модуля записи, а также сведения о сжатии и извлечении метаданных.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)