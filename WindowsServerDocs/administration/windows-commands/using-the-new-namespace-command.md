---
title: создать-пространство имен
description: Справочный раздел для New-Namespace, который создает и настраивает новое пространство имен.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6df60703-30bd-4d59-a8d9-9fe3efe96add
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7bc6b365da274fc62df3bb24375c07b97c8e4bc
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82710536"
---
# <a name="new-namespace"></a>создать-пространство имен

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Создает и настраивает новое пространство имен. Этот параметр следует использовать, если установлена только служба роли транспортного сервера. Если у вас установлена служба роли сервера развертывания и служба роли транспортного сервера (по умолчанию), используйте [команду New-мултикасттрансмиссион](using-the-new-multicasttransmission-command.md). Обратите внимание, что перед использованием этого параметра необходимо зарегистрировать поставщик содержимого.
## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /New-Namespace [/Server:<Server name>]
     /FriendlyName:<Friendly name>
     [/Description:<Description>]
     /Namespace:<Namespace name>
     /ContentProvider:<Name>
     [/ConfigString:<Configuration string>]
     /Namespacetype: {AutoCast | ScheduledCast}
         [/time:<YYYY/MM/DD:hh:mm>]
         [/Clients:<Number of clients>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server:<Server name>]|Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер.|
|FriendlyName<Friendly name>|Указывает понятное имя пространства имен.|
|/Description<Description>]|Задает описание пространства имен.|
|Имен<Namespace name>|Указывает имя пространства имен. Обратите внимание, что это не понятное имя, оно должно быть уникальным.<p>-   **Служба роли сервера развертывания**. для этого параметра используется следующий синтаксис:/namespace: WDS<Image group>/<Image name>/<Index>:. Например: **WDS: ImageGroup1/install. wim/1**<br />-   **Служба роли транспортного сервера**: это значение должно совпадать с именем, заданным при создании пространства имен на сервере.|
|/Контентпровидер:<Name>]|Указывает имя поставщика содержимого, который предоставит содержимое для пространства имен.|
|[/Конфигстринг:<Configuration string>]|Задает строку конфигурации для поставщика содержимого.|
|/Намеспацетипе: {автотрансляция &#124; Счедуледкаст}|Задает параметры передачи. Параметры задаются с помощью следующих параметров.<p>-[/Тиме: <time>] — задает время начала передачи с использованием следующего формата: гггг/мм/дд: чч: мм. Этот параметр применяется только к передачам по расписанию.<br />-[/Клиентс: <Number of clients>] — задает минимальное число клиентов для ожидания перед началом передачи. Этот параметр применяется только к передачам по расписанию.|
## <a name="examples"></a>Примеры
Чтобы создать пространство имен автоматического приведения, введите:
```
wdsutil /New-Namespace /FriendlyName:Custom AutoCast Namespace /Namespace:Custom Auto 1 /ContentProvider:MyContentProvider /Namespacetype:AutoCast
```
Чтобы создать пространство имен с расписанием, введите:
```
wdsutil /New-Namespace /Server:MyWDSServer /FriendlyName:Custom Scheduled Namespace /Namespace:Custom Auto 1 /ContentProvider:MyContentProvider 
/Namespacetype:ScheduledCast /time:2006/11/20:17:00 /Clients:20
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Ключ](command-line-syntax-key.md)
синтаксиса командной строки
[с помощью команды Get-аллнамеспацес](using-the-get-allnamespaces-command.md)[с помощью подкоманды Remove-Namespace](using-the-remove-namespace-command.md)
[. Start-Namespace.](subcommand-start-namespace.md)
