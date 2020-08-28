---
title: Подкоманда Start-Мултикасттрансмиссион
description: Справочная статья по подкоманде Start-Мултикасттрансмиссион, которая запускает пересылку образа по расписанию.
ms.topic: reference
ms.assetid: a1b2d459-1ece-49d4-997c-9d206c463b61
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91637f402fda0784672583a500f283bdde45e075
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024768"
---
# <a name="subcommand-start-multicasttransmission"></a>Подкоманда: Start-Мултикасттрансмиссион

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Запускает пересылку образа по расписанию.

## <a name="syntax"></a>Синтаксис
**Windows Server 2008**
```
wdsutil /start-MulticastTransmissiomedia:<Image name> [/Server:<Server namemediatype:InstallmediaGroup:<Image group name>] [/Filename:<File name>]
```
**Windows Server 2008 R2** для загрузочных образов:
```
wdsutil [Options] /start-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Boot
        /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
для образов установки:
```
wdsutil [Options] /start-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Install
       mediaGroup:<Image Group>]
        [/Filename:<File name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
носител<Image name>|Указывает имя образа.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
mediaType: {Установка&#124;Загрузка}|Указывает тип изображения. Обратите внимание, что этот параметр должен быть установлен для **установки** для Windows Server 2008.|
|/Арчитектуре: {x86 &#124; ia64 &#124; x64}|Архитектура загрузочного образа, связанного с передачей для запуска. Так как для образов загрузки можно использовать одно и то же имя образа в разных архитектурах, следует указать архитектуру, чтобы гарантировать использование правильной передачи.|
|\Медиаграуп: <Image group name> ]|Задает группу образов для образа. Если имя группы образов не указано и на сервере существует только одна группа образов, будет использоваться эта группа образов. Если на сервере существует несколько групп образов, необходимо использовать этот параметр, чтобы указать имя группы образов.|
|[/Филенаме: <File name> ]|Указывает имя файла, содержащего образ. Если образ не может быть однозначно идентифицирован по имени, необходимо использовать этот параметр, чтобы указать имя файла.|
## <a name="examples"></a>Примеры
Чтобы начать многоадресную передачу, введите одно из следующих действий:
```
wdsutil /start-MulticastTransmissiomedia:Vista with Office
/Imagetype:Install
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
Чтобы запустить многоадресную передачу образа загрузки для Windows Server 2008 R2, введите:
```
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:X64 Boot Imagemediatype:Boot /Architecture:x64
/Filename:boot.wim\n\
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-get-allmulticasttransmissions-command.md) 
 Get-аллмултикасттрансмиссионс [Использование команды](using-the-get-multicasttransmission-command.md) 
 Get-мултикасттрансмиссион [Использование команды](using-the-new-multicasttransmission-command.md) 
 New-мултикасттрансмиссион [Использование команды Remove-мултикасттрансмиссион](using-the-remove-multicasttransmission-command.md)
