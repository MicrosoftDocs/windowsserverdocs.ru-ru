---
title: WDSUTIL-транспортсервер
description: Справочная статья для Транспортсервер
ms.topic: reference
ms.assetid: dc1b1eec-6893-445e-81dc-16b3fae287fa
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6fd02b92316eee15bb3947eca6084cb43f514aad
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826130"
---
# <a name="wdsutil-stop-transportserver"></a>WDSUTIL-транспортсервер

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Останавливает все службы на транспортном сервере.
## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Stop-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя транспортного сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если транспортный сервер не указан, будет использоваться локальный сервер.|
## <a name="examples"></a>Примеры
Чтобы отключить службы, введите одно из следующих действий.
```
wdsutil /Stop-TransportServer
wdsutil /verbose /Stop-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Disable-транспортсервер](wdsutil-disable-transportserver.md)
- [Команда WDSUTIL Enable-транспортсервер](wdsutil-enable-transportserver.md)
- [Команда WDSUTIL Get-транспортсервер](wdsutil-get-transportserver.md)
- [Команда WDSUTIL Set-транспортсервер](wdsutil-set-transportserver.md)
- [Команда WDSUTIL Start-транспортсервер](wdsutil-start-transportserver.md)
