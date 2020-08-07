---
title: Get-Транспортсервер
description: Справочная статья по команде Get-Транспортсервер, которая отображает сведения о указанном транспортном сервере.
ms.topic: article
ms.assetid: de634123-0179-41b2-9c6f-726508130ff5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bebe03058544591d98dd827325b9740fb0fa65df
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896374"
---
# <a name="get-transportserver"></a>Get-Транспортсервер

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сведения о указанном транспортном сервере.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Get-TransportServer [/Server:<Server name>] /Show:{Config}
```
### <a name="parameters"></a>Параметры
|Параметр|Описание:|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
|/Show: {config}|Возвращает сведения о конфигурации указанного транспортного сервера.|
## <a name="examples"></a>Примеры
Чтобы просмотреть сведения о сервере, введите:
```
wdsutil /Get-TransportServer /Show:Config
```
Чтобы просмотреть сведения о конфигурации, введите:
```
wdsutil /Get-TransportServer /Server:MyWDSServer /Show:Config
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-disable-transportserver-command.md) 
 Disable-транспортсервер [Использование команды](using-the-enable-transportserver-command.md) 
 Enable-транспортсервер [Подкоманда: Set-транспортсервер](subcommand-set-transportserver.md) 
 [Подкоманда: Start-транспортсервер](subcommand-start-transportserver.md) 
 [Подкоманда: транспортсервер](subcommand-stop-transportserver.md)
