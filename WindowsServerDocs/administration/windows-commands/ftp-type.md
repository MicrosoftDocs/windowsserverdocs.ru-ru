---
title: ftp type
description: Справочная статья по команде типа FTP, которая задает или отображает тип перемещения файла.
ms.topic: reference
ms.assetid: 6e96dcd4-08f8-4e7b-90b7-1e1761fea4c7
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9a083ea3d43dcde2496563e4848bb7e44fc7acc7
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817308"
---
# <a name="ftp-type"></a>ftp type

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Задает или отображает тип перемещения файла. Команда **FTP** поддерживает как ASCII (по умолчанию), так и типы перемещения файлов с двоичными изображениями:

- При передаче текстовых файлов рекомендуется использовать ASCII. В режиме ASCII выполняется преобразование символов в стандартную сетевую кодировку и из нее. Например, символы конца строки при необходимости преобразуются в зависимости от целевой операционной системы.

- При передаче исполняемых файлов рекомендуется использовать двоичный формат. В двоичном режиме файлы передаются в однобайтовых единицах.

## <a name="syntax"></a>Синтаксис

```
type [<typename>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `[<typename>]` | Определяет тип передачи файла. Если этот параметр не указан, отображается текущий тип.|

### <a name="examples"></a>Примеры

Чтобы задать тип перемещения файла ASCII, введите:

```
type ascii
```

Чтобы задать тип файла для перемещения binary, введите:

```
type binary
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
