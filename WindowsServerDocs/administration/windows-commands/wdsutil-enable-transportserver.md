---
title: WDSUTIL Enable-транспортсервер
description: Справочная статья по WDSUTIL Enable-транспортсервер, которая включает все службы для транспортного сервера.
ms.topic: reference
ms.assetid: 9d79dba1-4b57-4a00-8cba-877e6b8618e6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4d4a294c0bda291e8340a4d8ffe54a11d487e0dd
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730943"
---
# <a name="wdsutil-enable-transportserver"></a>WDSUTIL Enable-транспортсервер

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Включает все службы для транспортного сервера.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Enable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя транспортного сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя не указано, будет использоваться локальный сервер.|
## <a name="examples"></a>Примеры
Чтобы включить службы на сервере, выполните одно из следующих действий.
```
wdsutil /Enable-TransportServer
wdsutil /verbose /Enable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Disable-транспортсервер](wdsutil-disable-transportserver.md)
- [Команда WDSUTIL Get-транспортсервер](wdsutil-get-transportserver.md)
- [Команда WDSUTIL Set-транспортсервер](wdsutil-set-transportserver.md)
- [Команда WDSUTIL Start-транспортсервер](wdsutil-start-transportserver.md)
- [Команда WDSUTIL транспортсервер](wdsutil-stop-transportserver.md)
