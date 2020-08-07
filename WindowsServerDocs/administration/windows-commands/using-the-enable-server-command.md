---
title: Enable-Server
description: Справочная статья по Enable-Server, которая включает все службы для служб развертывания Windows.
ms.topic: article
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 04884c4f4648db4ff78446048f34ea1ec609d154
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896550"
---
# <a name="enable-server"></a>Enable-Server

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Включает все службы для служб развертывания Windows.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Enable-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание:|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
## <a name="examples"></a>Примеры
Чтобы включить службы на сервере, выполните одно из следующих действий.
```
wdsutil /Enable-Server
wdsutil /verbose /Enable-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды «Disable-Server»](using-the-disable-server-command.md) 
 [Использование команды](using-the-get-server-command.md) 
 Get-Server [Использование команды](using-the-initialize-server-command.md) 
 Initialize-Server [Подкоманда: Set-Server](subcommand-set-server.md) 
 [Подкоманда: Start-Server](subcommand-start-server.md) 
 [Подкоманда:-сервер](subcommand-stop-server.md) 
 [Параметр Uninitialize-Server](the-uninitialize-server-option.md)
