---
title: WDSUTIL Start-транспортсервер
description: Справочная статья для подкоманды Start-Транспортсервер, которая запускает все службы для транспортного сервера.
ms.topic: reference
ms.assetid: 0e93bc84-5b9e-4f9d-8cf0-1634417da0f6
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 07ce12020ffd715e5077a9d49401e70d43d40fe2
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826163"
---
# <a name="wdsutil-start-transportserver"></a>WDSUTIL Start-транспортсервер

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Запускает все службы для транспортного сервера.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /start-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя транспортного сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
## <a name="examples"></a>Примеры
Чтобы запустить сервер, введите одно из следующих действий:
```
wdsutil /start-TransportServer
wdsutil /verbose /start-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Disable-транспортсервер](wdsutil-disable-transportserver.md)
- [Команда WDSUTIL Enable-транспортсервер](wdsutil-enable-transportserver.md)
- [Команда WDSUTIL Get-транспортсервер](wdsutil-get-transportserver.md)
- [Команда WDSUTIL Set-транспортсервер](wdsutil-set-transportserver.md)
- [Команда WDSUTIL транспортсервер](wdsutil-stop-transportserver.md)
