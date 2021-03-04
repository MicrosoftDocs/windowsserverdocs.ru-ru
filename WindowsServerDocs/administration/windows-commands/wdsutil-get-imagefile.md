---
title: Get-ImageFile
description: Справочная статья по Get-ImageFile, которая получает сведения об образах, содержащихся в WIM-файле образа Windows.
ms.topic: reference
ms.assetid: e1e296fb-20cf-4a60-9db4-4cbac7d4dab5
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 94205a21bdc1a2c2138e3eca45b9d98ea2d3ab35
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825148"
---
# <a name="get-imagefile"></a>Get-ImageFile

Извлекает сведения об образах, содержащихся в WIM-файле образа Windows.

## <a name="syntax"></a>Синтаксис

```
wdsutil [Options] /Get-ImageFile /ImageFile:<wim file path> [/Detailed]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|Изображения\<WIM file path>|Указывает полный путь и имя файла WIM.|
|[/Детаилед]|Возвращает все метаданные изображения из каждого изображения. Если этот параметр не используется, поведение по умолчанию — возврат только имени, описания и имени файла изображения.|

## <a name="examples"></a>Примеры

Чтобы просмотреть сведения об образе, введите:
```
wdsutil /Get-ImageFile /ImageFile:C:\temp\install.wim
```
Чтобы просмотреть подробные сведения, введите:
```
wdsutil /Verbose /Get-ImageFile /ImageFile:\\Server\Share\My Folder \install.wim /Detailed
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)