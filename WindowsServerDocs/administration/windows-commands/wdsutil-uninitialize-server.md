---
title: WDSUTIL Uninitialize-Server
description: Справочная статья для отмены инициализации сервера, которая возвращает изменения, внесенные в сервер во время первоначальной настройки сервера.
ms.topic: reference
ms.assetid: 015efb04-fe84-469f-bd81-49d0046296b2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7481c31c3dcd6cf6b76c26246fb9b103c7882d37
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826110"
---
# <a name="wdsutil-uninitialize-server"></a>WDSUTIL Uninitialize-Server

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Возвращает изменения, внесенные в сервер во время первоначальной настройки сервера. К ним относятся изменения, внесенные с помощью параметра **/инитиализе-сервер** или оснастки MMC служб развертывания Windows. Обратите внимание, что эта команда сбрасывает сервер в ненастроенное состояние. Эта команда не изменяет содержимое общей папки remoteInstall. Вместо этого он сбрасывает состояние сервера, чтобы можно было повторно инициализировать сервер.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Uninitialize-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
## <a name="examples"></a>Примеры
Чтобы повторно инициализировать сервер, введите одно из следующих действий:
```
wdsutil /Uninitialize-Server
wdsutil /verbose /Uninitialize-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Disable-Server](wdsutil-disable-server.md)
- [Команда WDSUTIL Enable-Server](wdsutil-enable-server.md)
- [Команда WDSUTIL Get-Server](wdsutil-get-server.md)
- [WDSUTIL Initialize-Server, команда](wdsutil-initialize-server.md)
- [Команда WDSUTIL Set-Server](wdsutil-set-server.md)
- [Команда WDSUTIL Start-Server](wdsutil-start-server.md)
- [Команда WDSUTIL-сервер](wdsutil-stop-server.md)
