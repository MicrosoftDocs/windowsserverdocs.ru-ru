---
title: Отклонить — Аутоадддевицес
description: Справочная статья по отклону Аутоадддевицес, которая отклоняет компьютеры, ожидающие административного утверждения.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea25a4b2-5fad-4360-9c47-c2c9df7ea31f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2b678f7a9fc875dfeebf735475db3adfb7ad9ae7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932420"
---
# <a name="reject-autoadddevices"></a>Отклонить — Аутоадддевицес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отклоняет компьютеры, ожидающие административного утверждения. Если включена политика автоматического добавления, то перед неизвестными компьютерами (не требующими предварительной подготовки) требуется административное утверждение, чтобы установить образ. Эту политику можно включить с помощью вкладки **Отклик PXE** страницы свойств сервера.
## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Reject-AutoaddDevices [/Server:<Server name>] /RequestId:<Request ID or ALL>
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
|/Рекуестид: идентификатор запроса <&#124; все>|Указывает идентификатор запроса, назначенный ожидающему компьютеру. Чтобы отклонить все ожидающие компьютеры, укажите **все**.|
## <a name="examples"></a>Примеры
Чтобы отклонить отдельный компьютер, введите:
```
wdsutil /Reject-AutoaddDevices /RequestId:12
```
Чтобы отклонить все компьютеры, введите:
```
wdsutil /verbose /Reject-AutoaddDevices /Server:MyWDSServer /RequestId:ALL
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-approve-autoadddevices-command.md) 
 "утвердить-аутоадддевицес" [Использование команды](using-the-delete-autoadddevices-command.md) 
 Delete-аутоадддевицес [Использование команды Get-аутоадддевицес](using-the-get-autoadddevices-command.md)
