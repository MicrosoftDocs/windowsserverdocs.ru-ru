---
title: WDSUTIL отклонения — аутоадддевицес
description: Справочная статья по WDSUTIL Reject-аутоадддевицес, которая отклоняет компьютеры, ожидающие административного утверждения.
ms.topic: reference
ms.assetid: ea25a4b2-5fad-4360-9c47-c2c9df7ea31f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2cb970ce6b51933e72f208f6fbcc50bcb7b3164b
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730692"
---
# <a name="wdsutil-reject-autoadddevices"></a>WDSUTIL отклонения — аутоадддевицес

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
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL утвердить-аутоадддевицес](wdsutil-approve-autoadddevices.md)
- [Команда WDSUTIL Delete-аутоадддевицес](wdsutil-delete-autoadddevices.md)
- [Команда WDSUTIL Get-аутоадддевицес](wdsutil-get-autoadddevices.md)
