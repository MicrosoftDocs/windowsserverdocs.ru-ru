---
title: WDSUTIL Delete — аутоадддевицес
description: Справочная статья по команде WDSUTIL Delete-аутоадддевицес, которая удаляет компьютеры, которые ожидают, отклонены или утверждены из базы данных автоматического добавления.
ms.topic: reference
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 68a4d7bfbc311ee0052fc360f4e05a47b94ed0e4
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825319"
---
# <a name="wdsutil-delete-autoadddevices"></a>WDSUTIL Delete — аутоадддевицес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет из базы данных автоматического добавления компьютеры, которые ожидают, отклонены или утверждены. Эта база данных хранит сведения об этих компьютерах на сервере.

## <a name="syntax"></a>Синтаксис

```
wdsutil /delete-AutoaddDevices [/Server:<Servername>] /Devicetype:{PendingDevices | RejectedDevices |ApprovedDevices}
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер. |
| Типа устройства`{PendingDevices|RejectedDevices|ApprovedDevices}` | Указывает тип компьютера, удаляемого из базы данных. Этот тип может быть **пендингдевицес**, который возвращает все компьютеры в базе данных с состоянием "ожидание", **режектеддевицес**, которое возвращает все компьютеры в базе данных с состоянием "Отклонено" или " **аппроведдевицес**", которое возвращает все компьютеры с состоянием "утверждено". |

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

- [Командлеты служб развертывания Windows](/powershell/module/wds)
