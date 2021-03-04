---
title: set metadata
description: Справочная статья по команде Set metadata, которая задает имя и расположение файла метаданных теневого копирования, используемого для перемещения теневых копий с одного компьютера на другой.
ms.topic: reference
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d3dc9e860c1fb43f54920eae27216297b7983e27
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805907"
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
