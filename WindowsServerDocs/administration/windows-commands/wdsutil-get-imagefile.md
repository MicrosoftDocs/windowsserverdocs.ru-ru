---
title: Get-ImageFile
description: Справочная статья по Get-ImageFile, которая получает сведения об образах, содержащихся в WIM-файле образа Windows.
ms.topic: reference
ms.assetid: e1e296fb-20cf-4a60-9db4-4cbac7d4dab5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 41183f92d75736afc32dfbbee9d31871b3ef24f9
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524339"
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