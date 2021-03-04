---
title: WDSUTIL Get-транспортсервер
description: Справочная статья по WDSUTIL Get-транспортсервер, в которой отображаются сведения о указанном транспортном сервере.
ms.topic: reference
ms.assetid: de634123-0179-41b2-9c6f-726508130ff5
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8bc0d032c00b391066a469f8d471e53ea6ae9275
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825761"
---
# <a name="wdsutil-get-transportserver"></a>WDSUTIL Get-транспортсервер

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
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Disable-транспортсервер](wdsutil-disable-transportserver.md)
- [Команда WDSUTIL Enable-транспортсервер](wdsutil-enable-transportserver.md)
- [Команда WDSUTIL Set-транспортсервер](wdsutil-set-transportserver.md)
- [Команда WDSUTIL Start-транспортсервер](wdsutil-start-transportserver.md)
- [Команда WDSUTIL транспортсервер](wdsutil-stop-transportserver.md)
