---
title: Запуск WDSUTIL-сервер
description: Справочная статья для команды Start-Server, запускающей все службы для сервера служб развертывания Windows.
ms.topic: reference
ms.assetid: 1e4343e2-0a16-4e65-8769-c09adaef5680
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3b123cb1ce7ffa8745f1eda4ee465bed40438388
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826193"
---
# <a name="wdsutil-start-server"></a>Запуск WDSUTIL-сервер

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Запускает все службы для сервера служб развертывания Windows.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /start-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера для запуска. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
## <a name="examples"></a>Примеры
Чтобы запустить сервер, введите одно из следующих действий:
```
wdsutil /start-Server
wdsutil /verbose /start-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Disable-Server](wdsutil-disable-server.md)
- [Команда WDSUTIL Enable-Server](wdsutil-enable-server.md)
- [Команда WDSUTIL Get-Server](wdsutil-get-server.md)
- [WDSUTIL Initialize-Server, команда](wdsutil-initialize-server.md)
- [Команда WDSUTIL Set-Server](wdsutil-set-server.md)
- [Команда WDSUTIL-сервер](wdsutil-stop-server.md)
- [Команда WDSUTIL Start-Server](wdsutil-start-server.md)
- [Команда WDSUTIL Uninitialize-Server](wdsutil-uninitialize-server.md)
