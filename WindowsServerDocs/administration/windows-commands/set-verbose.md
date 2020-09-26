---
title: set verbose
description: Справочная статья по команде Set Verbose, указывающей, следует ли предоставлять подробный вывод при создании теневой копии.
ms.topic: reference
ms.assetid: 93cb93c9-666f-4c74-814b-1c404a949935
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2e0b4d4cca66b20125c1aa0bbb67a7806133f6d8
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389046"
---
# <a name="set-verbose"></a>Задать verbose

Указывает, следует ли предоставлять подробный вывод при создании теневой копии. Если используется без параметров, команда **Set verbose** выводит справку из командной строки.

## <a name="syntax"></a>Синтаксис

```
set verbose {on | off}
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| on | Включает подробное ведение журнала вывода в процессе создания теневой копии. Если параметр verbose имеет значение ON, **параметр SET** предоставляет сведения о включении или исключении модуля записи, а также сведения о сжатии и извлечении метаданных. |
| off | Отключает подробный журнал вывода в процессе создания теневой копии. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда Set context](set-context.md)

- [команда задания метаданных](set-metadata.md)

- [команда Set Option](set-option.md)
