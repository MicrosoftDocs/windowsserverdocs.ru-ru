---
title: WDSUTIL Enable-Server
description: Справочная статья по команде WDSUTIL Enable-Server, которая включает все службы для служб развертывания Windows.
ms.topic: reference
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2e2f62198ce4c012245174bc00e536e15ecd1c27
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070326"
---
# <a name="wdsutil-enable-server"></a>WDSUTIL Enable-Server

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Включает все службы для служб развертывания Windows.

## <a name="syntax"></a>Синтаксис

```
wdsutil [options] /Enable-Server [/Server:<Servername>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер. |

## <a name="examples"></a>Примеры

Чтобы включить службы на сервере, введите:

```
wdsutil /Enable-Server
```

```
wdsutil /verbose /Enable-Server /Server:MyWDSServer
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Disable-Server](wdsutil-disable-server.md)

- [Команда WDSUTIL Get-Server](wdsutil-get-server.md)

- [WDSUTIL Initialize-Server, команда](wdsutil-initialize-server.md)

- [Команда WDSUTIL Set-Server](wdsutil-set-server.md)

- [Команда WDSUTIL Start-Server](wdsutil-start-server.md)

- [Команда WDSUTIL-сервер](wdsutil-stop-server.md)

- [Команда WDSUTIL Uninitialize-Server](wdsutil-uninitialize-server.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
