---
title: останавливаемый сервер WDSUTIL
description: Справочная статья для подкоманды Stop-Server, которая останавливает все службы на сервере служб развертывания Windows.
ms.topic: reference
ms.assetid: 09f411c0-099f-4591-95fd-b77b3fd9118a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1ad76c92c4077f23dbc4175d3a7a12007882bdc8
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826153"
---
# <a name="wdsutil-stop-server"></a>останавливаемый сервер WDSUTIL

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Останавливает все службы на сервере служб развертывания Windows.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Stop-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
## <a name="examples"></a>Примеры
Чтобы отключить службы, введите одно из следующих действий.
```
wdsutil /Stop-Server
wdsutil /verbose /Stop-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Disable-Server](wdsutil-disable-server.md)
- [Команда WDSUTIL Enable-Server](wdsutil-enable-server.md)
- [Команда WDSUTIL Get-Server](wdsutil-get-server.md)
- [WDSUTIL Initialize-Server, команда](wdsutil-initialize-server.md)
- [Команда WDSUTIL Set-Server](wdsutil-set-server.md)
- [Команда WDSUTIL Start-Server](wdsutil-start-server.md)
- [Команда WDSUTIL Uninitialize-Server](wdsutil-uninitialize-server.md)

