---
title: WDSUTIL Disable-транспортсервер
description: Справочная статья по команде WDSUTIL Disable-транспортсервер, которая отключает все службы для транспортного сервера.
ms.topic: reference
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4bbb177897e3a779de275957949b0dcf62e53478
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070356"
---
# <a name="wdsutil-disable-transportserver"></a>WDSUTIL Disable-транспортсервер

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отключает все службы для транспортного сервера.

## <a name="syntax"></a>Синтаксис

```
wdsutil [Options] /Disable-TransportServer [/Server:<Servername>]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|-------|--------|
|[/Server: `<Servername>` ]|Указывает имя транспортного сервера, который должен быть отключен. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя транспортного сервера не указано, будет использоваться локальный сервер.|

## <a name="examples"></a>Примеры

Чтобы отключить сервер, введите:

```
wdsutil /Disable-TransportServer
```

```
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Enable-транспортсервер](wdsutil-enable-transportserver.md)

- [Команда WDSUTIL Get-транспортсервер](wdsutil-get-transportserver.md)

- [Команда WDSUTIL Set-транспортсервер](wdsutil-set-transportserver.md)

- [Команда WDSUTIL Start-транспортсервер](wdsutil-start-transportserver.md)

- [Команда WDSUTIL транспортсервер](wdsutil-stop-transportserver.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
