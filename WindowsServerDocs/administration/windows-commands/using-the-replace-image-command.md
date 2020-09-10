---
title: Replace-Image
description: Справочная статья для Replace-Image, которая заменяет существующий образ новой версией этого образа.
ms.topic: reference
ms.assetid: 68ded3df-e309-420f-9f5d-caeb609385a5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0b6abc378f133670e33898693bb2b9f8b149a097
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636347"
---
# <a name="using-the-replace-image-command"></a>Использование команды replace-Image

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Заменяет существующий образ новой версией этого образа.
## <a name="syntax"></a>Синтаксис
для загрузочных образов:
```
wdsutil [Options] /replace-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Boot
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /replacementImage
       mediaFile:<wim file path>
         [/Name:<Image name>]
         [/Description:<Image description>]
```
для образов установки:
```
wdsutil [Options] /replace-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Install
    mediaGroup:<Image group name>]
     [/Filename:<File name>]
     /replacementImage
       mediaFile:<wim file path>
         [/SourceImage:<Source image name>]
         [/Name:<Image name>]
         [/Description:<Image description>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
носител<Image name>|Указывает имя заменяемого образа.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
mediaType: {Загрузка &#124; установка}|Указывает тип заменяемого образа.|
|/Арчитектуре: {x86 &#124; ia64 &#124; x64}|Указывает архитектуру заменяемого образа. Так как в разных архитектурах можно использовать одинаковое имя образа для разных образов загрузки, указание архитектуры гарантирует замену нужного образа.|
|[/Филенаме: <File name> ]|Если образ не может быть однозначно идентифицирован по имени, необходимо использовать этот параметр, чтобы указать имя файла.|
|/реплацементимаже|Задает параметры для замещающего изображения. Эти параметры задаются с помощью следующих параметров.<p>-mediaFile: <file path> — указывает имя и расположение (полный путь) для нового файла WIM.<br />-[/Саурцеимаже: <image name> ] — указывает образ, используемый, если WIM-файл содержит несколько образов. Этот параметр применяется только к образам установки.<br />-[/Name: <Image name> ] задает отображаемое имя образа.<br />-[/Description: <Image description> ] — задает описание образа.|
## <a name="examples"></a>Примеры
Чтобы заменить загрузочный образ, введите одно из следующих действий:
```
wdsutil /replace-Imagmedia:WinPE Boot Imagemediatype:Boot /Architecture:x86 /replacementImagmediaFile:C:\MyFolder\Boot.wim
wdsutil /verbose /Progress /replace-Imagmedia:WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim
/replacementImagmediaFile:\\MyServer\Share\Boot.wim /Name:My WinPE Image /Description:WinPE Image with drivers
```
Чтобы заменить образ установки, введите одно из следующих действий:
```
wdsutil /replace-Imagmedia:Windows Vista Homemediatype:Install /replacementImagmediaFile:C:\MyFolder\Install.wim
wdsutil /verbose /Progress /replace-Imagmedia:Windows Vista Pro /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1
/Filename:Install.wim /replacementImagmediaFile:\\MyServer\Share \Install.wim /SourceImage:Windows Vista Ultimate /Name:Windows Vista Desktop /Description:Windows Vista Ultimate with standard business applications.
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-add-image-command.md) 
 Add-Image [Использование команды](using-the-copy-image-command.md) 
 Copy-Image [Использование команды](using-the-export-image-command.md) 
 Export-Image [Использование команды](using-the-get-image-command.md) 
 Get-Image [Использование команды](using-the-replace-image-command.md) 
 Replace-Image [Подкоманда: Set-Image](subcommand-set-image.md)
