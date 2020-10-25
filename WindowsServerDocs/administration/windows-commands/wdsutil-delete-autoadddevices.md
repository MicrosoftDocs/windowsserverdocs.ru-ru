---
title: WDSUTIL Delete — аутоадддевицес
description: Справочная статья по команде WDSUTIL Delete-аутоадддевицес, которая удаляет компьютеры, которые ожидают, отклонены или утверждены из базы данных автоматического добавления.
ms.topic: reference
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 610b57c7db49c5d8cf354502634cf82212d52c19
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524819"
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
