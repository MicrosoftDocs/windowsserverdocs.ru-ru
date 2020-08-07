---
title: Delete — Аутоадддевицес
description: Справочная статья по Delete-Аутоадддевицес, которая удаляет компьютеры, которые ожидают, отклонены или утверждены из базы данных автоматического добавления.
ms.topic: article
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ccde56c5a0d3edd252048f9cf1e2a4b1fd28a35
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892175"
---
# <a name="delete-autoadddevices"></a>Delete — Аутоадддевицес

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
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-approve-autoadddevices-command.md) 
 "утвердить-аутоадддевицес" [Использование команды](using-the-get-autoadddevices-command.md) 
 Get-аутоадддевицес [Использование команды REJECT-аутоадддевицес](using-the-reject-autoadddevices-command.md)
