---
title: WDSUTIL Get-мултикасттрансмиссион
description: Справочная статья по WDSUTIL Get-мултикасттрансмиссион, в которой отображаются сведения о передаче многоадресной рассылки для указанного образа.
ms.topic: reference
ms.assetid: b733737b-1e81-43d4-a058-d6985a613bef
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bed732f6aeae3c59a8a060bee37d206ef22e4773
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825118"
---
# <a name="wdsutil-get-multicasttransmission"></a>WDSUTIL Get-мултикасттрансмиссион

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сведения о передаче многоадресной рассылки для указанного образа.

## <a name="syntax"></a>Синтаксис
**Windows Server 2008**
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>]
[/Filename:<File name>] [/Show:Clients]
```
**Windows Server 2008 R2** для передачи загрузочных образов:
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
    [/Server:<Server name>]
    [/details:Clients]
  mediatype:Boot
    /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
для передачи образов установки:
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
         [/Server:<Server name>]
         [/details:Clients]
       mediatype:Install
    mediaGroup:<Image Group>]
     [/Filename:<File name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
носител<Image name>|Отображает многоадресную передачу, связанную с этим образом.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер.|
|/с: Установка|Указывает тип изображения. Обратите внимание, что этот параметр должен быть установлен в значение **Install**.|
|/имажеграуп: <Image group name> ]|Указывает группу образов, содержащую образ. Если имя группы образов не указано и на сервере существует только одна группа образов, используется эта группа образов. Если на сервере существует несколько групп образов, необходимо использовать этот параметр, чтобы указать группу образов.|
|/Арчитектуре: {x86 &#124; ia64 &#124; x64}|Указывает архитектуру загрузочного образа, связанного с передачей. Так как для образов загрузки можно использовать одно и то же имя образа в разных архитектурах, следует указать архитектуру, чтобы гарантировать использование правильного образа.|
|[/Филенаме: <File name> ]|Указывает файл, содержащий изображение. Если образ не может быть однозначно идентифицирован по имени, необходимо использовать этот параметр, чтобы указать имя файла.|
|[/Show: Clients]<p>или диспетчер конфигурации служб<p>[/детаилс: клиенты]|Отображает сведения о клиентских компьютерах, подключенных к многоадресной передаче.|
## <a name="examples"></a>Примеры
**Windows Server 2008** Чтобы просмотреть сведения о передаче образа под названием Vista с Office, введите одно из следующих действий:
```
wdsutil /Get-MulticastTransmission:Vista with Office imagetype:Install
wdsutil /Get-MulticastTransmission /Server:MyWDSServer image:Vista with Office imagetype:Install imageGroup:ImageGroup1 /Filename:install.wim /Show:Clients
```
**Windows Server 2008 R2** Чтобы просмотреть сведения о передаче образа под названием Vista с Office, введите одно из следующих действий:
```
wdsutil /Get-MulticastTransmission:Vista with Office
 /Imagetype:Install
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServer image:Vista with Office imagetype:Install ImageGroup:ImageGroup1 /Filename:install.wim /details:Clients
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServer:X64 Boot Imagetype:Boot /Architecture:x64 /Filename:boot.wim /details:Clients
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Get-аллмултикасттрансмиссионс](wdsutil-get-allmulticasttransmissions.md)
- [Команда WDSUTIL New-мултикасттрансмиссион](wdsutil-new-multicasttransmission.md)
- [Команда WDSUTIL Remove-мултикасттрансмиссион](wdsutil-remove-multicasttransmission.md)
- [Команда WDSUTIL Start-мултикасттрансмиссион](wdsutil-start-multicasttransmission.md)
