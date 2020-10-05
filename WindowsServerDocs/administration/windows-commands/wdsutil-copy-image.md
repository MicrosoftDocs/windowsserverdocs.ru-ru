---
title: WDSUTIL Copy-Image
description: Справочная статья по WDSUTIL Copy-Image, которая копирует образы, которые находятся в одной и той же группе образов.
ms.topic: reference
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a04848d0b673697809af08b91ca91856d6491773
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91731007"
---
# <a name="wdsutil-copy-image"></a>WDSUTIL Copy-Image

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Копирует образы, которые находятся в одной и той же группе образов. Чтобы скопировать изображения между группами образов, используйте команду [вдсутилекспорт-Image](wdsutil-export-image.md) , а затем команду [вдсутиладд-Image](wdsutil-add-image.md) .

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /copy-Image image:<Image name> [/Server:<Server name>]
    imagetype:Install
     imageGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Name:<Name>
         /Filename:<File name>
         [/Description:<Description>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
| Эскиз<Image name>|Задает имя копируемого образа.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
| ImageType: install|Указывает тип копируемого изображения. Этот параметр должен быть установлен в значение " **установить**".|
|\Имажеграуп: <Image group name> ]|Указывает группу образов, содержащую копируемый образ. Если группа образов не указана и на сервере существует только одна группа, то эта группа образов будет использоваться по умолчанию. Если на сервере существует более одной группы образов, необходимо указать группу образов.|
|[/Филенаме: <Filename> ]|Указывает имя файла копируемого образа. Если исходный образ не может быть однозначно определен по имени, необходимо указать имя файла.|
|/дестинатионимаже|Задает параметры для конечного образа, как описано в следующей таблице.<p>-/Name: <Name> -задает отображаемое имя копируемого образа.<br />-/Филенаме: <Filename> — задает имя конечного файла образа, который будет содержать копию образа.<br />-[/Description: <Description>] — Задает описание копии образа.|
## <a name="examples"></a>Примеры
Чтобы создать копию указанного образа и назовите ее Виндовсвиста. wim, введите:
```
wdsutil /copy-Image image:Windows Vista with Office imagetype:Install /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim
```
Чтобы создать копию указанного образа, примените указанные параметры и назовите копию Виндовсвиста. wim, введите:
```
wdsutil /verbose /Progress /copy-Image image:Windows Vista with Office /Server:MyWDSServe imagetype:Install imageGroup:ImageGroup1
/Filename:install.wim /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim /Description:This is a copy of the original Windows image with Office installed
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Add-Image](wdsutil-add-image.md)
- [Команда WDSUTIL Export-Image](wdsutil-export-image.md)
- [Команда WDSUTIL Get-Image](wdsutil-get-image.md)
- [Команда WDSUTIL Remove-Image](wdsutil-remove-image.md)
- [Команда WDSUTIL Replace-Image](wdsutil-replace-image.md)
- [Команда WDSUTIL Set-Image](wdsutil-set-image.md)
