---
title: WDSUTIL Get-аутоадддевицес
description: Справочная статья по WDSUTIL Get-аутоадддевицес, в которой отображаются все компьютеры, которые находятся в базе данных автоматического добавления на сервере служб развертывания Windows.
ms.topic: reference
ms.assetid: 24b4b688-55b0-4bd9-a2f5-7ef4b3dfe2f2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e7d24786d2a24702f233993e59650fd2d7751bce
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825861"
---
# <a name="wdsutil-get-autoadddevices"></a>WDSUTIL Get-аутоадддевицес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает все компьютеры, которые находятся в базе данных автоматического добавления на сервере служб развертывания Windows.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
|/Девицетипе: {Пендингдевицес &#124; Режектеддевицес &#124; Аппроведдевицес}|Указывает тип возвращаемого компьютера.<p>-   **Пендингдевицес** возвращает все компьютеры в базе данных с состоянием "ожидание".<br />-   **Режектеддевицес** возвращает все компьютеры в базе данных, состояние которых было отклонено.<br />-   **Аппроведдевицес** возвращает все компьютеры в базе данных, имеющие состояние "утверждено".|
## <a name="examples"></a>Примеры
Чтобы просмотреть список всех утвержденных компьютеров, введите:
```
wdsutil /Get-AutoaddDevices /Devicetype:ApprovedDevices
```
Чтобы просмотреть список всех отклоненных компьютеров, введите:
```
wdsutil /verbose /Get-AutoaddDevices /Devicetype:RejectedDevices /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Delete-аутоадддевицес](wdsutil-delete-autoadddevices.md)
- [Команда WDSUTIL утвердить-аутоадддевицес](wdsutil-approve-autoadddevices.md)
- [Команда WDSUTIL Reject-аутоадддевицес](wdsutil-reject-autoadddevices.md)
