---
title: Copy-Image
description: Справочная статья по Copy-Image, которая копирует образы, которые находятся в одной и той же группе образов.
ms.topic: article
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4995d45de3897c590dd232b316756330081b13ee
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892193"
---
# <a name="copy-image"></a>Copy-Image

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Копирует образы, которые находятся в одной и той же группе образов. Для копирования образов между группами образов используйте команду [Export-Image](using-the-export-image-command.md) , а затем команду [Add-Image](using-the-add-image-command.md) .

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /copy-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Install
    mediaGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Name:<Name>
         /Filename:<File name>
         [/Description:<Description>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание:|
|-------|--------|
носител<Image name>|Задает имя копируемого образа.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
mediaType: Установка|Указывает тип копируемого изображения. Этот параметр должен быть установлен в значение " **установить**".|
|\Медиаграуп: <Image group name> ]|Указывает группу образов, содержащую копируемый образ. Если группа образов не указана и на сервере существует только одна группа, то эта группа образов будет использоваться по умолчанию. Если на сервере существует более одной группы образов, необходимо указать группу образов.|
|[/Филенаме: <Filename> ]|Указывает имя файла копируемого образа. Если исходный образ не может быть однозначно определен по имени, необходимо указать имя файла.|
|/дестинатионимаже|Задает параметры для конечного образа, как описано в следующей таблице.<p>-/Name: <Name> -задает отображаемое имя копируемого образа.<br />-/Филенаме: <Filename> — задает имя конечного файла образа, который будет содержать копию образа.<br />-[/Description: <Description>] — Задает описание копии образа.|
## <a name="examples"></a>Примеры
Чтобы создать копию указанного образа и назовите ее Виндовсвиста. wim, введите:
```
wdsutil /copy-Imagmedia:Windows Vista with Officemediatype:Install /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim
```
Чтобы создать копию указанного образа, примените указанные параметры и назовите копию Виндовсвиста. wim, введите:
```
wdsutil /verbose /Progress /copy-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim /Description:This is a copy of the original Windows image with Office installed
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-add-image-command.md) 
 Add-Image [Использование команды](using-the-export-image-command.md) 
 Export-Image [Использование команды](using-the-get-image-command.md) 
 Get-Image [Использование команды](using-the-remove-image-command.md) 
 Remove-Image [Использование команды](using-the-replace-image-command.md) 
 Replace-Image [Подкоманда: Set-Image](subcommand-set-image.md)
