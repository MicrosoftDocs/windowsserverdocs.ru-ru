---
title: Remove-Мултикасттрансмиссион
description: Справочная статья по Remove-Мултикасттрансмиссион, которая отключает многоадресную передачу изображения.
ms.topic: article
ms.assetid: 9a7f5c31-bfbf-425d-9129-a6f9173fe83d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8c3de852ab09b2cc17badf9b3aefcca9b7f4d069
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891918"
---
# <a name="using-the-remove-multicasttransmission-command"></a>Использование команды Remove-Мултикасттрансмиссион

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отключает передачу многоадресной рассылки для образа. Если не указать **/Force**, существующие клиенты будут выполнять перенос образа, но новые клиенты не смогут присоединяться.

## <a name="syntax"></a>Синтаксис
**Windows Server 2008**
```
wdsutil /remove-MulticastTransmissiomedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image Group>] [/Filename:<File name>] [/force]
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
|Параметр|Описание:|
|-------|--------|
носител<Image name>|Указывает имя образа.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер.|
mediaType: {Установка&#124;Загрузка}|Указывает тип изображения. Обратите внимание, что этот параметр должен быть установлен для **установки** для Windows Server 2008.|
|/Арчитектуре: {x86 &#124; ia64 &#124; x64}|Указывает архитектуру загрузочного образа, связанного с передачей для запуска. Так как для образов загрузки в разных архитектурах можно использовать одно и то же имя образа, следует указать архитектуру, чтобы гарантировать использование правильной передачи.|
|\Медиаграуп: <Image group name> ]|Указывает группу образов, содержащую образ. Если имя группы образов не указано и на сервере существует только одна группа образов, используется эта группа образов. Если на сервере существует несколько групп образов, необходимо использовать этот параметр, чтобы указать имя группы образов.|
|[/Филенаме: <File name> ]|Указывает имя файла. Если исходный образ не может быть однозначно определен по имени, необходимо использовать этот параметр, чтобы указать имя файла.|
|/Force|удаляет передачу и завершает работу всех клиентов. Если не указано значение параметра **/Force** , существующие клиенты могут завершить перенос образа, но новые клиенты не смогут присоединиться.|
## <a name="examples"></a>Примеры
Для завершения передачи пространства имен (текущие клиенты будут выполнять передачу, но новые клиенты не смогут присоединиться) введите:
```
wdsutil /remove-MulticastTransmissiomedia:Vista with Office
/Imagetype:Install
```
```
wdsutil /remove-MulticastTransmissiomedia:x64 Boot Image
/Imagetype:Boot /Architecture:x64
```
Для принудительного завершения работы всех клиентов введите:
```
wdsutil /remove-MulticastTransmission /Server:MyWDSServer
/Image:Vista with Officemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /force
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-get-allmulticasttransmissions-command.md) 
 Get-аллмултикасттрансмиссионс [Использование команды](using-the-get-multicasttransmission-command.md) 
 Get-мултикасттрансмиссион [Использование команды](using-the-new-multicasttransmission-command.md) 
 New-мултикасттрансмиссион [Подкоманда: Start-мултикасттрансмиссион](subcommand-start-multicasttransmission.md)
