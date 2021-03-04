---
title: WDSUTIL Enable-транспортсервер
description: Справочная статья по команде WDSUTIL Enable-транспортсервер, которая включает все службы для транспортного сервера.
ms.topic: reference
ms.assetid: 9d79dba1-4b57-4a00-8cba-877e6b8618e6
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b270641eaa98306424c717d8e4621ad24433be76
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101803779"
---
# <a name="wdsutil-enable-transportserver"></a>WDSUTIL Enable-транспортсервер

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Включает все службы для транспортного сервера.

## <a name="syntax"></a>Синтаксис

```
wdsutil [options] /Enable-TransportServer [/Server:<Servername>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер. |

## <a name="examples"></a>Примеры

Чтобы включить службы на сервере, введите:

```
wdsutil /Enable-TransportServer
```

```
wdsutil /verbose /Enable-TransportServer /Server:MyWDSServer
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Disable-транспортсервер](wdsutil-disable-transportserver.md)

- [Команда WDSUTIL Get-транспортсервер](wdsutil-get-transportserver.md)

- [Команда WDSUTIL Set-транспортсервер](wdsutil-set-transportserver.md)

- [Команда WDSUTIL Start-транспортсервер](wdsutil-start-transportserver.md)

- [Команда WDSUTIL транспортсервер](wdsutil-stop-transportserver.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
