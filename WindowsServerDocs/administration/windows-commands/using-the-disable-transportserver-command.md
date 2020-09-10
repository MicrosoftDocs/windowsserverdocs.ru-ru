---
title: Disable-Транспортсервер
description: Справочная статья по Disable-Транспортсервер, которая отключает все службы для транспортного сервера.
ms.topic: reference
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2fd2ac1c346aca8132870edea2bf7696114089b2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622000"
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
