---
title: WDSUTIL Get-Image
description: Справочная статья по WDSUTIL Get-Image, которая получает сведения о изображении.
ms.topic: reference
ms.assetid: 0ecaa999-72ad-4191-adb5-a418de42a001
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b7d57e031df85f1ba8c9e61d6532105fe690b679
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826543"
---
# <a name="wdsutil-get-image"></a>WDSUTIL Get-Image

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Извлекает сведения о изображении.

## <a name="syntax"></a>Синтаксис
для загрузочных образов:
```
wdsutil [Options] /Get-Image image:<Image name> [/Server:<Server name> imagetype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
```
для образов установки:
```
wdsutil [Options] /Get-image image:<Image name> [/Server:<Server name> imagetype:Install imagegroup:<Image group name>] [/Filename:<File name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
| Эскиз<Image name>|Указывает имя образа.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
| ImageType: {Boot &#124; install}|Указывает тип изображения.|
|/Арчитектуре: {x86 &#124; ia64 &#124; x64}|Указывает архитектуру образа. Так как для образов загрузки в разных архитектурах можно использовать одно и то же имя образа, задание значения архитектуры гарантирует, что будет возвращен правильный образ.|
|[/Филенаме: <File name> ]|Если образ не может быть однозначно идентифицирован по имени, необходимо использовать этот параметр, чтобы указать имя файла.|
|\имажеграуп: <Image group name> ]|Указывает группу образов, содержащую образ. Если группа образов не указана и на сервере существует только одна группа образов, будет использоваться эта группа. Если на сервере существует несколько групп образов, необходимо использовать этот параметр, чтобы указать группу образов.|
## <a name="examples"></a>Примеры
Чтобы получить сведения о загрузочном образе, введите один из следующих элементов:
```
wdsutil /Get-Image image:WinPE boot imagetype:Boot /Architecture:x86
wdsutil /verbose /Get-Image image:WinPE boot image /Server:MyWDSServer imagetype:Boot /Architecture:x86 /Filename:boot.wim
```
Чтобы получить сведения о образе установки, введите одно из следующих действий:
```
wdsutil /Get-Image:Windows Vista with Office imagetype:Install
wdsutil /verbose /Get-Image:Windows Vista with Office /Server:MyWDSServer imagetype:Install imagegroup:ImageGroup1 /Filename:install.wim
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Add-Image](wdsutil-add-image.md)
- [Команда WDSUTIL Copy-Image](wdsutil-copy-image.md)
- [Команда WDSUTIL Export-Image](wdsutil-export-image.md)
- [Команда WDSUTIL Remove-Image](wdsutil-remove-image.md)
- [Команда WDSUTIL Replace-Image](wdsutil-replace-image.md)
- [Команда WDSUTIL Set-Image](wdsutil-set-image.md)
