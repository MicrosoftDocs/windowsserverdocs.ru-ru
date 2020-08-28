---
title: Подкоманда Start-Server
description: Справочная статья для команды Start-Server, запускающей все службы для сервера служб развертывания Windows.
ms.topic: reference
ms.assetid: 1e4343e2-0a16-4e65-8769-c09adaef5680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d79ef2689f15a0f6fdc67cf5c068372f6f448c7
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024748"
---
# <a name="subcommand-start-server"></a>Подкоманда: Start-Server

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
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды «Disable-Server»](using-the-disable-server-command.md) 
 [Использование команды](using-the-enable-server-command.md) 
 Enable-Server [Использование команды](using-the-get-server-command.md) 
 Get-Server [Использование команды](using-the-initialize-server-command.md) 
 Initialize-Server [Подкоманда: Set-Server](subcommand-set-server.md) 
 [Подкоманда:-сервер](subcommand-stop-server.md) 
 [Параметр Uninitialize-Server](the-uninitialize-server-option.md)
