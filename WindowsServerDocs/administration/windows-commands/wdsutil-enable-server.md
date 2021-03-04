---
title: WDSUTIL Enable-Server
description: Справочная статья по команде WDSUTIL Enable-Server, которая включает все службы для служб развертывания Windows.
ms.topic: reference
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2b24bb83baa47b569349946e57a58951dd8a2ec5
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101803807"
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
