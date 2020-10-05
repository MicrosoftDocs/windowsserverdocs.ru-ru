---
title: WDSUTIL Remove-Image
description: Справочная статья по WDSUTIL Remove-Image, которая удаляет образ с сервера.
ms.topic: reference
ms.assetid: ce5e2384-2264-4b22-92af-74eec8c10ae0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f1d955f54f345b6d2832eabe2334dd77f32633e7
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91731238"
---
# <a name="wdsutil-remove-image"></a>WDSUTIL Remove-Image

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет образ с сервера.

## <a name="syntax"></a>Синтаксис
для загрузочных образов:
```
wdsutil [Options] /remove-Image:<Image name> [/Server:<Server name> type:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<Filename>]
```
для образов установки:
```
wdsutil [Options] /remove-image:<Image name> [/Server:<Server name> type:Install ImageGroup:<Image group name>] [/Filename:<Filename>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
| /ремове-имаже:<Image name>|Указывает имя образа.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
mediaType: {Загрузка &#124; установка}|Указывает тип изображения.|
|/Арчитектуре: {x86 &#124; ia64 &#124; x64}|Указывает архитектуру образа. Так как в разных архитектурах для разных образов загрузки можно использовать одинаковое имя образа, задание значения архитектуры гарантирует, что будет удален нужный образ.|
|\Имажеграуп: <Image group name> ]|Указывает группу образов, содержащую образ. Если имя группы образов не указано и на сервере существует только одна группа образов, будет использоваться эта группа образов. Если существует несколько групп образов, необходимо использовать этот параметр, чтобы указать группу образов.|
|[/Филенаме: <File name> ]|Если образ не может быть однозначно идентифицирован по имени, необходимо использовать этот параметр, чтобы указать имя файла.|
## <a name="examples"></a>Примеры
Чтобы удалить загрузочный образ, введите:
```
wdsutil /remove-Imagmedia:WinPE Boot Imagemediatype:Boot /Architecture:x86
```
```
wdsutil /verbose /remove-Image:WinPE Boot Image /Server:MyWDSServer type:Boot /Architecture:x64 /Filename:boot.wim
```
Чтобы удалить образ установки, введите:
```
wdsutil /remove-Image:Windows Vista with Officemediatype:Install
```
```
wdsutil /verbose /remove-Image:Windows Vista with Office /Server:MyWDSServemediatype:Instal ImageGroup:ImageGroup1 /Filename:install.wim
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Add-Image](wdsutil-add-image.md)
- [Команда WDSUTIL Copy-Image](wdsutil-copy-image.md)
- [Команда WDSUTIL Export-Image](wdsutil-export-image.md)
- [Команда WDSUTIL Get-Image](wdsutil-get-image.md)
- [Команда WDSUTIL Replace-Image](wdsutil-replace-image.md)
- [Команда WDSUTIL Set-Image](wdsutil-set-image.md)
