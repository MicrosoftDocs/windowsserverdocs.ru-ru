---
title: Get-Транспортсервер
description: Справочная статья по команде Get-Транспортсервер, которая отображает сведения о указанном транспортном сервере.
ms.topic: reference
ms.assetid: de634123-0179-41b2-9c6f-726508130ff5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 83b79c689e16af16e0a6ca253dd9dce6afb1fa35
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029492"
---
# <a name="get-transportserver"></a>Get-Транспортсервер

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сведения о указанном транспортном сервере.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Get-TransportServer [/Server:<Server name>] /Show:{Config}
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
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
