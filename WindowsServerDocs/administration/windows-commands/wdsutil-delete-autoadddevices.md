---
title: WDSUTIL Delete — аутоадддевицес
description: Справочная статья по WDSUTIL Delete-аутоадддевицес, которая удаляет компьютеры, которые ожидают, отклонены или утверждены из базы данных автоматического добавления.
ms.topic: reference
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 98c5aa38fd5394d4060cf9eba874d1be5cef845b
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730996"
---
# <a name="wdsutil-delete-autoadddevices"></a>WDSUTIL Delete — аутоадддевицес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет из базы данных автоматического добавления компьютеры, которые ожидают, отклонены или утверждены. Эта база данных хранит сведения об этих компьютерах на сервере.

## <a name="syntax"></a>Синтаксис
```
wdsutil /delete-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices |ApprovedDevices}
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
|/Девицетипе: {Пендингдевицес &#124; Режектеддевицес &#124;Аппроведдевицес}|Указывает тип компьютера, удаляемого из базы данных. Это может быть любой из следующих трех типов:<p>-   **Пендингдевицес** возвращает все компьютеры в базе данных с состоянием "ожидание".<br />-   **Режектеддевицес** возвращает все компьютеры в базе данных, состояние которых было отклонено.<br />-   **Аппроведдевицес** возвращает все компьютеры с состоянием "утверждено".|
## <a name="examples"></a>Примеры
Чтобы удалить все отклоненные компьютеры, введите:
```
wdsutil /delete-AutoaddDevices /Devicetype:RejectedDevices
```
Чтобы удалить все утвержденные компьютеры, введите:
```
wdsutil /verbose /delete-AutoaddDevices /Server:MyWDSServer /Devicetype:ApprovedDevices
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL утвердить-аутоадддевицес](wdsutil-approve-autoadddevices.md)
- [Команда WDSUTIL Get-аутоадддевицес](wdsutil-get-autoadddevices.md)
- [Команда WDSUTIL Reject-аутоадддевицес](wdsutil-reject-autoadddevices.md)
