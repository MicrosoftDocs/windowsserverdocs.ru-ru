---
title: WDSUTIL Copy-Image
description: Справочная статья по команде WDSUTIL Copy-Image, которая копирует образы, которые находятся в одной и той же группе образов.
ms.topic: reference
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0848906431aac66061c75affd1dc8ddfdf09471f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101803967"
---
# <a name="wdsutil-copy-image"></a>WDSUTIL Copy-Image

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Копирует образы, которые находятся в одной и той же группе образов. Чтобы скопировать изображения между группами образов, используйте команду [wdsutil Export-Image](wdsutil-export-image.md) , а затем команду [WDSUTIL Add-Image](wdsutil-add-image.md) .

## <a name="syntax"></a>Синтаксис

```
wdsutil [Options] /copy-Image image:<Image name> [/Server:<Server name>] imagetype:Install imageGroup:<Image group name>] [/Filename:<File name>] /DestinationImage /Name:<Name> /Filename:<File name> [/Description:<Description>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| Эскиз`<Imagename>` | Задает имя копируемого образа. |
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер. |
| ImageType: install | Указывает тип копируемого изображения. Этот параметр должен быть установлен в значение " **установить**". |
| \Имажеграуп: `<Image groupname>` ] | Указывает группу образов, содержащую копируемый образ. Если группа образов не указана и на сервере существует только одна группа, то эта группа образов используется по умолчанию. Если на сервере существует более одной группы образов, необходимо указать группу образов. |
| [/Филенаме: `<Filename>` ] | Указывает имя файла копируемого образа. Если исходный образ не может быть однозначно определен по имени, необходимо указать имя файла. |
| /дестинатионимаже | Задает параметры для конечного образа. Допустимые значения:<ul><li>/Name: `<Name>` — задает отображаемое имя копируемого образа.</li><li>/Филенаме: `<Filename>` — задает имя конечного файла образа, который будет содержать копию образа.</li><li>[/Description: `<Description>` ] — Задает описание копии образа.</li></ul> |

## <a name="examples"></a>Примеры

Чтобы создать копию указанного образа и назовите ее Виндовсвиста. wim, введите:

```
wdsutil /copy-Image image:Windows Vista with Office imagetype:Install /DestinationImage /Name:copy of Windows Vista with Office / Filename:WindowsVista.wim
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

- [Командлеты служб развертывания Windows](/powershell/module/wds)
