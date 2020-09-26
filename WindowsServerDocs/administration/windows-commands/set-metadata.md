---
title: set metadata
description: Справочная статья по команде Set metadata, которая задает имя и расположение файла метаданных теневого копирования, используемого для перемещения теневых копий с одного компьютера на другой.
ms.topic: reference
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2ff03661d953ae7afc39117ced89734c5df02c14
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389078"
---
# <a name="set-metadata"></a>set metadata

Задает имя и расположение файла метаданных теневого копирования, используемого для перемещения теневых копий с одного компьютера на другой. Если используется без параметров, **параметр SET Metadata** отображает справку в командной строке.

## <a name="syntax"></a>Синтаксис

```
set metadata [<drive>:][<path>]<metadata.cab>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `[<drive>:][<path>]` | Указывает расположение для создания файла метаданных. |
| `<metadata.cab>` | Указывает имя CAB-файла для хранения метаданных создания теневой копии. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда Set context](set-context.md)

- [команда Set Option](set-option.md)

- [команда Set verbose](set-verbose.md)
