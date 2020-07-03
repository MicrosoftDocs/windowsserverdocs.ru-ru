---
title: Набор подкоманд-Image
description: Справочная статья по подкоманде Set-Image, которая изменяет атрибуты изображения.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ae03c86-7a13-4e38-9182-32e55fffd504
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fcf77f34a35a56c872948568071d36c1fcf5940f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937161"
---
# <a name="subcommand-set-image"></a>Подкоманда: Set-Image

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет атрибуты изображения.

## <a name="syntax"></a>Синтаксис
для загрузочных образов:
```
wdsutil /Set-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>] [/Name:<Name>]
[/Description:<Description>] [/Enabled:{Yes | No}]
```
для образов установки:
```
wdsutil /Set-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:InstallmediaGroup:<Image group name>]
     [/Filename:<File name>]
     [/Name:<Name>]
     [/Description:<Description>]
     [/UserFilter:<SDDL>]
     [/Enabled:{Yes | No}]
     [/UnattendFile:<Unattend file path>]
         [/OverwriteUnattend:{Yes | No}]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
носител<Image name>|Указывает имя образа.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
mediaType: {Загрузка &#124; установка}|Указывает тип изображения.|
|/Арчитектуре: {x86 &#124; ia64 &#124; x64}|Указывает архитектуру образа. Поскольку одно и то же имя образа можно использовать для разных образов загрузки в разных архитектурах, указание архитектуры гарантирует, что образ будет изменен.|
|[/Филенаме: <File name> ]|Если образ не может быть однозначно идентифицирован по имени, необходимо использовать этот параметр, чтобы указать имя файла.|
|/Name|Указывает имя образа.|
|/Description<Description>]|Задает описание образа.|
|[/Enabled: {Yes &#124; No}]|Включает или отключает образ.|
|\Медиаграуп: <Image group name> ]|Указывает группу образов, содержащую образ. Если имя группы образов не указано и на сервере существует только одна группа образов, будет использоваться эта группа образов. Если на сервере существует несколько групп образов, необходимо использовать этот параметр, чтобы указать группу образов.|
|[/Усерфилтер: <SDDL> ]|Задает фильтр пользователя на изображении. Строка фильтра должна быть в формате языка определения дескрипторов безопасности (SDDL). Обратите внимание, что, в отличие от параметра **/секурити** для групп образов, этот параметр запрещает только те, кто может видеть определение образа, а не фактические ресурсы файла изображения. Чтобы ограничить доступ к файловым ресурсам и, следовательно, доступ ко всем образам в группе образов, необходимо настроить безопасность для самой группы образов.|
|[/Unattendfile.: <Unattend file path> ]|Задает полный путь к файлу автоматической установки, который должен быть связан с изображением. Например: **D:\Files\Unattend\Img1Unattend.xml**|
|[/Овервритеунаттенд: {Yes &#124; No}]|Можно указать параметр **/overwrite** , чтобы перезаписать файл автоматической установки, если файл автоматической установки, связанный с этим образом, уже существует. Обратите внимание, что значение по умолчанию — **нет**.|
## <a name="examples"></a>Примеры
Чтобы задать значения для загрузочного образа, введите одно из следующих значений:
```
wdsutil /Set-Imagmedia:WinPE boot imagemediatype:Boot /Architecture:x86 /Description:New description
wdsutil /verbose /Set-Imagmedia:WinPE boot image /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim
/Name:New Name /Description:New Description /Enabled:Yes
```
Чтобы задать значения для образа установки, введите одно из следующих значений:
```
wdsutil /Set-Imagmedia:Windows Vista with Officemediatype:Install /Description:New description
wdsutil /verbose /Set-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /Name:New name /Description:New description /UserFilter:O:BAG:DUD:AI(A;ID;FA;;;SY)(A;ID;FA;;;BA)(A;ID;0x1200a9;;;AU) /Enabled:Yes /UnattendFile:\\server\share\unattend.xml /OverwriteUnattend:Yes
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-add-image-command.md) 
 Add-Image [Использование команды](using-the-copy-image-command.md) 
 Copy-Image [Использование команды](using-the-export-image-command.md) 
 Export-Image [Использование команды](using-the-get-image-command.md) 
 Get-Image [Использование команды](using-the-remove-image-command.md) 
 Remove-Image [Использование команды replace-Image](using-the-replace-image-command.md)
