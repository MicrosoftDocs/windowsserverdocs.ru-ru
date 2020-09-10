---
title: Задание метаданных
description: Справочная статья по заданию метаданных, которая задает имя и расположение файла метаданных теневого копирования, используемого для перемещения теневых копий с одного компьютера на другой.
ms.topic: reference
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b680ac538f7c2593871137b07d045ef150b68b1f
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637684"
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