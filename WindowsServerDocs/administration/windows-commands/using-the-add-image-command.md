---
title: добавить-изображение
description: Справочная статья по Add-Image, которая добавляет образы на сервер служб развертывания Windows.
ms.topic: article
ms.assetid: d5b6f4da-90ba-4b0e-9423-66c8ef5172e2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 24afd8b608875fcb971efad50d4c8adf16541557
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896996"
---
# <a name="add-image"></a>добавить-изображение

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет образы на сервер служб развертывания Windows.

## <a name="syntax"></a>Синтаксис
для загрузочных образов используйте следующий синтаксис:
```
wdsutil /add-ImagmediaFile:<wim file path> [/Server:<Server name>mediatype:Boot [/Skipverify] [/Name:<Image name>] [/Description:<Image description>]
[/Filename:<New wim file name>]
```
для образов установки используйте следующий синтаксис:
```
wdsutil /add-ImagmediaFile:<wim file path>
     [/Server:<Server name>]
   mediatype:Install
     [/Skipverify]
    mediaGroup:<Image group name>]
     [/SingleImage:<Single image name>]
         [/Name:<Name>]
         [/Description:<Description>]
     [/Filename:<File name>]
     [/UnattendFile:<Unattend file path>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
mediaFile: путь к файлу <. wim>|Указывает полный путь и имя файла образа Windows (WIM-файла), содержащего добавляемые образы.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
mediaType: {Загрузка&#124;установка}|Указывает тип добавляемых образов.|
|[/Скипверифи]|Указывает, что проверка целостности не будет выполняться для исходного файла изображения перед добавлением образа.|
|[/Name: <Name> ]|Задает отображаемое имя изображения.|
|/Description<Description>]|Задает описание образа.|
|[/Филенаме: <Filename> ]|Указывает новое имя файла для WIM-файла. Это позволяет изменить имя файла WIM при добавлении образа. Если имя файла не указано, будет использоваться имя файла исходного изображения. Во всех случаях службы развертывания Windows проверяют, является ли имя файла уникальным в хранилище загрузочных образов конечного компьютера.|
|\Медиаграуп: <Image group name> ]|Указывает имя группы образов, в которую будут добавлены образы. Если на сервере существует более одной группы образов, необходимо указать группу образов. Если этот элемент не указан и группа образов еще не существует, будет создана новая группа образов. В противном случае будет использоваться существующая группа образов.|
|[/Синглеимаже: <Single image name> ] [/Name: <Name> ] /Description<Description>]|Копирует указанный отдельный образ из WIM-файла и задает отображаемое имя и описание образа.|
|[/Unattendfile.: <Unattend file path> ]|Указывает полный путь к файлу автоматической установки, который будет связан с добавляемыми изображениями. Если **/синглеимаже** не указан, то тот же файл автоматической установки будет связан со всеми образами в WIM-файле.|
## <a name="examples"></a>Примеры
Чтобы добавить загрузочный образ, введите:
```
wdsutil /add-ImagmediaFile:C:\MyFolder\Boot.wimmediatype:Boot
wdsutil /verbose /Progress /add-ImagmediaFile:\\MyServer\Share\Boot.wim /Server:MyWDSServemediatype:Boot /Name:My WinPE Image
/Description:WinPE Image containing the WDS Client /Filename:WDSBoot.wim
```
Чтобы добавить образ установки, введите одно из следующих действий:
```
wdsutil /add-ImagmediaFile:C:\MyFolder\Install.wimmediatype:Install
wdsutil /verbose /Progress /add-ImagmediaFile:\\MyServer\Share \Install.wim /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1
/SingleImage:Windows Pro /Name:My WDS Image
/Description:Windows Pro image with Microsoft Office /Filename:Win Pro.wim /UnattendFile:\\server\share\unattend.xml
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-copy-image-command.md) 
 Copy-Image [Использование команды](using-the-export-image-command.md) 
 Export-Image [Использование команды](using-the-get-image-command.md) 
 Get-Image [Использование команды](using-the-remove-image-command.md) 
 Remove-Image [Использование команды](using-the-replace-image-command.md) 
 Replace-Image [Подкоманда: Set-Image](subcommand-set-image.md)
