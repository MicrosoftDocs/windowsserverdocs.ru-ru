---
title: Задание метаданных
description: Справочная статья по заданию метаданных, которая задает имя и расположение файла метаданных теневого копирования, используемого для перемещения теневых копий с одного компьютера на другой.
ms.topic: reference
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dabec963b84a5c8d5acfd5e214b8d62d4740d9b3
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024948"
---
# <a name="set-metadata"></a>Задание метаданных

Задает имя и расположение файла метаданных теневого копирования, используемого для перемещения теневых копий с одного компьютера на другой. Если используется без параметров, **параметр SET Metadata** отображает справку в командной строке.

## <a name="syntax"></a>Синтаксис

```
set metadata [<Drive>:][<Path>]<MetaData.cab>
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|[\<Drive>:][<Path>]|Указывает расположение для создания файла метаданных.|
|\<MetaData.cab>|Указывает имя CAB-файла для хранения метаданных создания теневой копии.|

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)