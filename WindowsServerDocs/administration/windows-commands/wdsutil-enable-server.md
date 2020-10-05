---
title: WDSUTIL Enable-Server
description: Справочная статья по WDSUTIL Enable-Server, которая включает все службы для служб развертывания Windows.
ms.topic: reference
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3ec32f2bd0d269795e1f88b967804c2bb82ac9f4
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730948"
---
# <a name="wdsutil-enable-server"></a>WDSUTIL Enable-Server

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Включает все службы для служб развертывания Windows.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Enable-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
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
 Команда WDSUTIL disable [-Server](wdsutil-disable-server.md) 
 Команда WDSUTIL Get [-Server](wdsutil-get-server.md) 
 [WDSUTIL Initialize-Server, команда](wdsutil-initialize-server.md) 
 Команда WDSUTIL Set [-Server](wdsutil-set-server.md) 
 Команда WDSUTIL Start [-Server](wdsutil-start-server.md) 
 Команда WDSUTIL- [сервер](wdsutil-stop-server.md) 
 [команда WDSUTIL Uninitialize-Server](wdsutil-uninitialize-server.md)
