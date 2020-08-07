---
title: Disable-Транспортсервер
description: Справочная статья по Disable-Транспортсервер, которая отключает все службы для транспортного сервера.
ms.topic: article
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 48909ffb5a452d4bac1058acc5ddc48ed69b371f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892117"
---
# <a name="disable-transportserver"></a>Disable-Транспортсервер

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отключает все службы для транспортного сервера.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Disable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя транспортного сервера, который должен быть отключен. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя транспортного сервера не указано, будет использоваться локальный сервер.|
## <a name="examples"></a>Примеры
Чтобы отключить сервер, введите:
```
wdsutil /Disable-TransportServer
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-enable-transportserver-command.md) 
 Enable-транспортсервер [Использование команды](using-the-get-transportserver-command.md) 
 Get-транспортсервер [Подкоманда: Set-транспортсервер](subcommand-set-transportserver.md) 
 [Подкоманда: Start-транспортсервер](subcommand-start-transportserver.md) 
 [Подкоманда: транспортсервер](subcommand-stop-transportserver.md)
