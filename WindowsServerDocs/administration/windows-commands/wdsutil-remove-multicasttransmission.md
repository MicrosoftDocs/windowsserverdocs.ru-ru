---
title: WDSUTIL Remove-мултикасттрансмиссион
description: Справочная статья по WDSUTIL Remove-мултикасттрансмиссион, которая отключает многоадресную передачу изображения.
ms.topic: reference
ms.assetid: 9a7f5c31-bfbf-425d-9129-a6f9173fe83d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a7ed8d9ef26deb0a50baa8511cd07f250561d579
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91731378"
---
# <a name="wdsutil-remove-multicasttransmission"></a>WDSUTIL Remove-мултикасттрансмиссион

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отключает передачу многоадресной рассылки для образа. Если не указать **/Force**, существующие клиенты будут выполнять перенос образа, но новые клиенты не смогут присоединяться.

## <a name="syntax"></a>Синтаксис
**Windows Server 2008**
```
wdsutil /remove-MulticastTransmission:<Image name> [/Server:<Server name> mediatype:Install Group:<Image Group>] [/Filename:<File name>] [/force]
```
**Windows Server 2008 R2** для загрузочных образов:
```
wdsutil [Options] /remove-MulticastTransmissiomedia:<Image name>
\x20    [/Server:<Server name>]
\x20  mediatype:Boot
\x20    /Architecture:{x86 | ia64 | x64}
\x20    [/Filename:<File name>]
```
для образов установки:
```
wdsutil [Options] /remove-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Install
       mediaGroup:<Image Group
        [/Filename:<File name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|носител<Image name>|Указывает имя образа.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер.|
mediaType: {Установка&#124;Загрузка}|Указывает тип изображения. Обратите внимание, что этот параметр должен быть установлен для **установки** для Windows Server 2008.|
|/Арчитектуре: {x86 &#124; ia64 &#124; x64}|Указывает архитектуру загрузочного образа, связанного с передачей для запуска. Так как для образов загрузки в разных архитектурах можно использовать одно и то же имя образа, следует указать архитектуру, чтобы гарантировать использование правильной передачи.|
|\Медиаграуп: <Image group name> ]|Указывает группу образов, содержащую образ. Если имя группы образов не указано и на сервере существует только одна группа образов, используется эта группа образов. Если на сервере существует несколько групп образов, необходимо использовать этот параметр, чтобы указать имя группы образов.|
|[/Филенаме: <File name> ]|Указывает имя файла. Если исходный образ не может быть однозначно определен по имени, необходимо использовать этот параметр, чтобы указать имя файла.|
|/Force|удаляет передачу и завершает работу всех клиентов. Если не указано значение параметра **/Force** , существующие клиенты могут завершить перенос образа, но новые клиенты не смогут присоединиться.|
## <a name="examples"></a>Примеры
Для завершения передачи пространства имен (текущие клиенты будут выполнять передачу, но новые клиенты не смогут присоединиться) введите:
```
wdsutil /remove-MulticastTransmission:Vista with Office
/Imagetype:Install
```
```
wdsutil /remove-MulticastTransmission:x64 Boot Image
/Imagetype:Boot /Architecture:x64
```
Для принудительного завершения работы всех клиентов введите:
```
wdsutil /remove-MulticastTransmission /Server:MyWDSServer
/Image:Vista with Officemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /force
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Get-аллмултикасттрансмиссионс](wdsutil-get-allmulticasttransmissions.md)
- [Команда WDSUTIL Get-мултикасттрансмиссион](wdsutil-get-multicasttransmission.md)
- [Команда WDSUTIL New-мултикасттрансмиссион](wdsutil-new-multicasttransmission.md)
- [Команда WDSUTIL Start-мултикасттрансмиссион](wdsutil-start-multicasttransmission.md)
