---
title: WDSUTIL New-мултикасттрансмиссион
description: Справочная статья по WDSUTIL New-мултикасттрансмиссион, которая создает новую многоадресную передачу для образа.
ms.topic: reference
ms.assetid: c1f1dc46-dd50-4eb9-9f72-cf0e5d71bd3d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5e362caf76cbfeed91ca20bcaa96cfc023a6092c
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825681"
---
# <a name="wdsutil-new-multicasttransmission"></a>WDSUTIL New-мултикасттрансмиссион

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Создает новую многоадресную передачу для образа. Эта команда эквивалентна созданию передачи с помощью оснастки MMC для служб развертывания Windows (щелкните правой кнопкой мыши узел **многоадресные** передачи и выберите команду **Создать многоадресную передачу**). Эту команду следует использовать при наличии установленной службы роли сервера развертывания и службы роли транспортного сервера (установка по умолчанию). Если установлена только служба роли транспортного сервера, используйте [команду вдсутилнев-Namespace](wdsutil-new-namespace.md).
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
      imagetype:Install
       ImageGroup:<Image Group>]
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
      imagetype:Boot
        /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
| /Image<Image name>|Указывает имя изображения, которое должно быть передано с помощью многоадресной рассылки.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
|FriendlyName<Friendly name>|Указывает понятное имя передачи.|
|/Description<Description>]|Задает описание передачи.|
| Системное: {Загрузка&#124;установка}|Указывает тип изображения, передаваемого с помощью многоадресной рассылки. Примечание. **Загрузка** поддерживается только для Windows Server 2008 R2.|
| /Имажеграуп: <Image group name> ]|Указывает группу образов, содержащую образ. Если имя группы образов не указано и на сервере существует только одна группа образов, используется эта группа образов. Если на сервере существует несколько групп образов, необходимо использовать этот параметр, чтобы указать имя группы образов.|
|[/Филенаме: <File name> ]|Указывает имя файла. Если исходный образ не может быть однозначно определен по имени, необходимо использовать этот параметр, чтобы указать имя файла.|
|/Трансмиссионтипе: {автотрансляция &#124; Счедуледкаст}|Указывает, следует ли начинать передачу автоматически (автотрансляцию) или на основе указанных критериев запуска (Счедуледкаст).<p><ul><li>**Автоматическое приведение**. Этот тип передачи указывает, что как только соответствующий клиент запрашивает установочный образ, начинается многоадресная передача выбранного образа. Поскольку другие клиенты запрашивают тот же образ, они присоединяются к уже запущенной передаче.</li><li>**Запланированное приведение**. Этот тип передачи задает критерий запуска для передачи на основе числа клиентов, запрашивающих образ, и/или определенного дня и времени. Можно задать следующие параметры:<p><ul><li>[/Тиме: <time> ] — Задает время начала передачи с использованием следующего формата: гггг/мм/дд: чч: мм.</li><li>[/Клиентс: <Number of clients> ] — Задает минимальное число клиентов, ожидающих перед началом передачи.</li></ul></li></ul>|
|/Арчитектуре: {x86 &#124; ia64 &#124; x64}|Указывает архитектуру загрузочного образа для передачи с помощью многоадресной рассылки. Так как для образов загрузки различных архитектур можно использовать одно и то же имя, необходимо указать архитектуру для обеспечения правильного использования образа.|
|[/Филенаме: <File name> ]|Указывает имя файла. Если исходный образ не может быть однозначно определен по имени, необходимо указать имя файла.|
## <a name="examples"></a>Примеры
Чтобы создать автоматическую передачу образа загрузки в Windows Server 2008 R2, введите:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS Boot Transmission
/Image:X64 Boot imagetype:Boot /Architecture:x64 /Transmissiontype:AutoCast
```
Чтобы создать автоматическую передачу образа установки, введите:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS AutoCast Transmission
/Image:Vista with Officeimage imagetype:Install /Transmissiontype:AutoCast
```
Чтобы создать Scheduled-Castную передачу образа установки, введите:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS SchedCast Transmission /Server:MyWDSServer Image:Vista with Office imagetype:Install
/Transmissiontype:ScheduledCast /time:2006/11/20:17:00 /Clients:100
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Get-аллмултикасттрансмиссионс](wdsutil-get-allmulticasttransmissions.md)
- [Команда WDSUTIL Get-мултикасттрансмиссион](wdsutil-get-multicasttransmission.md)
- [Команда WDSUTIL Remove-мултикасттрансмиссион](wdsutil-remove-multicasttransmission.md)
- [Команда WDSUTIL Start-мултикасттрансмиссион](wdsutil-start-multicasttransmission.md)
