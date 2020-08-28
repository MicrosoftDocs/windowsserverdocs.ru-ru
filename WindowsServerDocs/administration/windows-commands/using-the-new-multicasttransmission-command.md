---
title: New-Мултикасттрансмиссион
description: Справочная статья по New-Мултикасттрансмиссион, которая создает новую многоадресную передачу для образа.
ms.topic: reference
ms.assetid: c1f1dc46-dd50-4eb9-9f72-cf0e5d71bd3d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30988ad23151f12533b75323f9376859a4c5d2a5
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038152"
---
# <a name="new-multicasttransmission"></a>New-Мултикасттрансмиссион

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Создает новую многоадресную передачу для образа. Эта команда эквивалентна созданию передачи с помощью оснастки MMC для служб развертывания Windows (щелкните правой кнопкой мыши узел **многоадресные** передачи и выберите команду **Создать многоадресную передачу**). Эту команду следует использовать при наличии установленной службы роли сервера развертывания и службы роли транспортного сервера (установка по умолчанию). Если установлена только служба роли транспортного сервера, используйте [команду New-Namespace](using-the-new-namespace-command.md).
## <a name="syntax"></a>Синтаксис
для передач образов установки:
```
wdsutil [Options] /New-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
        /FriendlyName:<Friendly name>
        [/Description:<Description>]
        /Transmissiontype: {AutoCast | ScheduledCast}
            [/time:<YYYY/MM/DD:hh:mm>]
            [/Clients:<Num of Clients>]
      mediatype:Install
       mediaGroup:<Image Group>]
        [/Filename:<File name>]
```
для передач загрузочных образов (поддерживается только для Windows Server 2008 R2):
```
wdsutil [Options] /New-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
        /FriendlyName:<Friendly name>
        [/Description:<Description>]
        /Transmissiontype: {AutoCast | ScheduledCast}
            [/time:<YYYY/MM/DD:hh:mm>]
            [/Clients:<Num of Clients>]
      mediatype:Boot
        /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
носител<Image name>|Указывает имя изображения, которое должно быть передано с помощью многоадресной рассылки.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
|FriendlyName<Friendly name>|Указывает понятное имя передачи.|
|/Description<Description>]|Задает описание передачи.|
mediaType: {Загрузка&#124;установка}|Указывает тип изображения, передаваемого с помощью многоадресной рассылки. Примечание. **Загрузка** поддерживается только для Windows Server 2008 R2.|
|\Медиаграуп: <Image group name> ]|Указывает группу образов, содержащую образ. Если имя группы образов не указано и на сервере существует только одна группа образов, используется эта группа образов. Если на сервере существует несколько групп образов, необходимо использовать этот параметр, чтобы указать имя группы образов.|
|[/Филенаме: <File name> ]|Указывает имя файла. Если исходный образ не может быть однозначно определен по имени, необходимо использовать этот параметр, чтобы указать имя файла.|
|/Трансмиссионтипе: {автотрансляция &#124; Счедуледкаст}|Указывает, следует ли начинать передачу автоматически (автотрансляцию) или на основе указанных критериев запуска (Счедуледкаст).<p><ul><li>**Автоматическое приведение**. Этот тип передачи указывает, что как только соответствующий клиент запрашивает установочный образ, начинается многоадресная передача выбранного образа. Поскольку другие клиенты запрашивают тот же образ, они присоединяются к уже запущенной передаче.</li><li>**Запланированное приведение**. Этот тип передачи задает критерий запуска для передачи на основе числа клиентов, запрашивающих образ, и/или определенного дня и времени. Можно задать следующие параметры:<p><ul><li>[/Тиме: <time> ] — Задает время начала передачи с использованием следующего формата: гггг/мм/дд: чч: мм.</li><li>[/Клиентс: <Number of clients> ] — Задает минимальное число клиентов, ожидающих перед началом передачи.</li></ul></li></ul>|
|/Арчитектуре: {x86 &#124; ia64 &#124; x64}|Указывает архитектуру загрузочного образа для передачи с помощью многоадресной рассылки. Так как для образов загрузки различных архитектур можно использовать одно и то же имя, необходимо указать архитектуру для обеспечения правильного использования образа.|
|[/Филенаме: <File name> ]|Указывает имя файла. Если исходный образ не может быть однозначно определен по имени, необходимо указать имя файла.|
## <a name="examples"></a>Примеры
Чтобы создать автоматическую передачу образа загрузки в Windows Server 2008 R2, введите:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS Boot Transmission
/Image:X64 Boot Imagemediatype:Boot /Architecture:x64 /Transmissiontype:AutoCast
```
Чтобы создать автоматическую передачу образа установки, введите:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS AutoCast Transmission
/Image:Vista with Officemediatype:Install /Transmissiontype:AutoCast
```
Чтобы создать запланированную передачу образа установки, введите:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS SchedCast Transmission /Server:MyWDSServemedia:Vista with Officemediatype:Install
/Transmissiontype:ScheduledCast /time:2006/11/20:17:00 /Clients:100
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-get-allmulticasttransmissions-command.md) 
 Get-аллмултикасттрансмиссионс [Использование команды](using-the-get-multicasttransmission-command.md) 
 Get-мултикасттрансмиссион [Использование команды](using-the-remove-multicasttransmission-command.md) 
 Remove-мултикасттрансмиссион [Подкоманда: Start-мултикасттрансмиссион](subcommand-start-multicasttransmission.md)
