---
title: WDSUTIL Add-Image
description: Справочная статья по команде WDSUTIL Add-Image, которая добавляет образы на сервер служб развертывания Windows.
ms.topic: reference
ms.assetid: d5b6f4da-90ba-4b0e-9423-66c8ef5172e2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3544e2e7443e55b14abddf2538e34d221ba41171
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804127"
---
# <a name="wdsutil-add-image"></a>WDSUTIL Add-Image

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет образы на сервер служб развертывания Windows.

## <a name="syntax"></a>Синтаксис

Для загрузочных образов используйте следующий синтаксис:

```
wdsutil /add-Image imageFile:<wim file path> [/Server:<Server name> imagetype:Boot [/Skipverify] [/Name:<Image name>] [/Description:<Image description>] [/Filename:<New wim file name>]
```

Для образов установки используйте следующий синтаксис:

```
wdsutil /add-Image imageFile:<wim filepath> [/Server:<Servername>] imagetype:Install [/Skipverify] imageGroup:<Image group name>] [/SingleImage:<Single image name>] [/Name:<Name>] [/Description:<Description>] [/Filename:<File name>] [/UnattendFile:<Unattend file path>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| Изображения`<.wim filepath>` | Указывает полный путь и имя файла образа Windows (WIM-файла), содержащего добавляемые образы. |
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер. |
| ImageType`{Boot|Install}` | Указывает тип добавляемых образов. |
| [/Скипверифи] | Указывает, что проверка целостности не будет выполняться для исходного файла изображения перед добавлением образа. |
| [/Name: `<Name>` ] | Задает отображаемое имя изображения. |
| [/Description: `<Description>` ] | Задает описание образа. |
| [/Филенаме: `<Filename>` ] | Указывает новое имя файла для WIM-файла. Это позволяет изменить имя файла WIM при добавлении образа. Если имя файла не указано, используется исходное имя файла образа. Во всех случаях службы развертывания Windows проверяют, является ли имя файла уникальным в хранилище загрузочных образов конечного компьютера. |
| \Имажеграуп: `<Imagegroupname>` ] | Указывает имя группы образов, в которую будут добавлены образы. Если на сервере существует более одной группы образов, необходимо указать группу образов. Если не указать группу образов, а группа образов еще не существует, создается новая группа образов. В противном случае используется существующая группа образов. |
| [/Синглеимаже: `<Singleimagename>` ] [/Name: `<Name>` ] [/Description: `<Description>` ] | Копирует указанный отдельный образ из WIM-файла и задает отображаемое имя и описание образа. |
| [/Unattendfile.: `<Unattendfilepath>` ] | Указывает полный путь к файлу автоматической установки, который будет связан с добавляемыми изображениями. Если **/синглеимаже** не указан, то тот же файл автоматической установки связан со всеми образами в WIM-файле. |

## <a name="examples"></a>Примеры

Чтобы добавить загрузочный образ, введите:

```
wdsutil /add-Image imageFile:C:\MyFolder\Boot.wim imagetype:Boot
wdsutil /verbose /Progress /add-Image imageFile:\\MyServer\Share\Boot.wim /Server:MyWDSServer imagetype:Boot /Name:My WinPE Image /Description:WinPE Image containing the WDS Client /Filename:WDSBoot.wim
```

Чтобы добавить образ установки, введите одно из следующих действий:

```
wdsutil /add-Image imageFile:C:\MyFolder\Install.wim imagetype:Install
wdsutil /verbose /Progress /add-Image imageFile:\\MyServer\Share \Install.wim /Server:MyWDSServer imagetype:Instal imageGroup:ImageGroup1
/SingleImage:Windows Pro /Name:My WDS Image /Description:Windows Pro image with Microsoft Office /Filename:Win Pro.wim /UnattendFile:\\server\share\unattend.xml
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Copy-Image](wdsutil-copy-image.md)

- [Команда WDSUTIL Export-Image](wdsutil-export-image.md)

- [Команда WDSUTIL Get-Image](wdsutil-get-image.md)

- [Команда WDSUTIL Remove-Image](wdsutil-remove-image.md)

- [Команда WDSUTIL Replace-Image](wdsutil-replace-image.md)

- [Команда WDSUTIL Set-Image](wdsutil-set-image.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
