---
title: WDSUTIL Export-Image
description: Справочная статья по команде WDSUTIL Export-Image, которая экспортирует существующий образ из хранилища образов в другой файл образа Windows (WIM).
ms.topic: reference
ms.assetid: a9b8b467-0f2d-4754-8998-55503a262778
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8c3c390e43cc8707d8d94ade757130276b5f2753
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93071046"
---
# <a name="wdsutil-export-image"></a>WDSUTIL Export-Image

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Экспортирует существующий образ из хранилища образов в другой файл образа Windows (WIM).

## <a name="syntax"></a>Синтаксис

Для загрузочных образов:

```
wdsutil [options] /Export-Image image:<Image name> [/Server:<Servername>]
    imagetype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<Filename>]
     /DestinationImage
         /Filepath:<Filepath and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No}]
```

Для образов установки:

```
wdsutil [options] /Export-Image image:<Image name> [/Server:<Servername>]
    imagetype:Install imageGroup:<Image group name>]
     [/Filename:<Filename>]
     /DestinationImage
         /Filepath:<Filepath and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No | append}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| Эскиз`<Imagename>` | Указывает имя экспортируемого образа. |
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер. |
| ImageType`{Boot|Install}` | Указывает тип экспортируемого изображения. |
| \Имажеграуп: `<Image group name>` ] | Указывает группу образов, содержащую экспортируемый образ. Если имя группы образов не указано и на сервере существует только одна группа образов, то эта группа образов будет использоваться по умолчанию. Если на сервере существует более одной группы образов, необходимо указать группу образов. |
| AHA`{x86|ia64|x64}` | Определяет архитектуру экспортируемого образа. Так как для образов загрузки в разных архитектурах можно использовать одно и то же имя образа, задание значения архитектуры гарантирует, что будет возвращен правильный образ. |
| [/Филенаме: `<Filename>` ] | Если образ не может быть однозначно определен по имени, необходимо указать имя файла. |
| /дестинатионимаже | Задает параметры для конечного образа. Эти параметры можно указать с помощью следующих параметров.<ul><li>`/Filepath:<Filepath and name>` — Указывает полный путь к файлу для нового образа.</li><li>`[/Name:<Name>]` — Задает отображаемое имя образа. Если имя не указано, будет использоваться отображаемое имя исходного изображения.</li><li>`[/Description: <Description>]` — Задает описание образа.</li></ul> |
| [/Overwrite: `{Yes|No|append}` ] | Определяет, будет ли перезаписан файл, указанный в параметре **/дестинатионимаже** , если существующий файл с таким именем уже существует в/филепас. Параметр **Да** приводит к перезаписи существующего файла, параметр **No** (по умолчанию) вызывает ошибку, если файл с таким именем уже существует, а параметр **append** приводит к добавлению созданного образа в качестве нового образа в существующий WIM-файл. |

## <a name="examples"></a>Примеры

Чтобы экспортировать загрузочный образ, введите:

```
wdsutil /Export-Image image:WinPE boot image imagetype:Boot /Architecture:x86 /DestinationImage /Filepath:C:\temp\boot.wim
```

```
wdsutil /verbose /Progress /Export-Image image:WinPE boot image /Server:MyWDSServer imagetype:Boot /Architecture:x64 /Filename:boot.wim /DestinationImage /Filepath:\\Server\Share\ExportImage.wim /Name:Exported WinPE image /Description:WinPE Image from WDS server /Overwrite:Yes
```

Чтобы экспортировать образ установки, введите:

```
wdsutil /Export-Image image:Windows Vista with Office imagetype:Install /DestinationImage /Filepath:C:\Temp\Install.wim
```

```
wdsutil /verbose /Progress /Export-Image image:Windows Vista with Office /Server:MyWDSServer imagetype:Instal imageGroup:ImageGroup1 /Filename:install.wim /DestinationImage /Filepath:\\server\share\export.wim /Name:Exported Windows image /Description:Windows Vista image from WDS server /Overwrite:append
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Add-Image](wdsutil-add-image.md)

- [Команда WDSUTIL Copy-Image](wdsutil-copy-image.md)

- [Команда WDSUTIL Get-Image](wdsutil-get-image.md)

- [Команда WDSUTIL Remove-Image](wdsutil-remove-image.md)

- [Команда WDSUTIL Replace-Image](wdsutil-replace-image.md)

- [Команда WDSUTIL Set-Image](wdsutil-set-image.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)