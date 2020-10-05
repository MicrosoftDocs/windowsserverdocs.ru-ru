---
title: WDSUTIL Get-аллдевицес
description: Справочная статья по WDSUTIL Get-аллдевицес, в которой отображаются свойства служб развертывания Windows для всех предварительно подготовленных компьютеров.
ms.topic: reference
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 57d565a0b4b79efd3a472505db5f57ecc0ba564f
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730919"
---
# <a name="wdsutil-get-alldevices"></a>WDSUTIL Get-аллдевицес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает свойства служб развертывания Windows для всех предварительно подготовленных компьютеров. Предварительно подготовленный компьютер — это физический компьютер, связанный с учетной записью компьютера в доменных службах Active Directory.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Get-AllDevices [/forest:{Yes | No}] [/ReferralServer:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Forest: {Да &#124; No}]|Указывает, должны ли службы развертывания Windows возвращать компьютеры во всем лесу или в локальном домене. Значение по умолчанию — « **нет**». Это означает, что возвращаются только компьютеры в локальном домене.|
|[/Реферралсервер: <Server name> ]|Возвращает только те компьютеры, которые предварительно подготовлены для указанного сервера.|
## <a name="examples"></a>Примеры
Чтобы просмотреть все компьютеры, введите одно из следующих действий:
```
wdsutil /Get-AllDevices
wdsutil /verbose /Get-AllDevices /forest:Yes /ReferralServer:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Set-Device](wdsutil-set-device.md)
- [Команда WDSUTIL Add-Device](wdsutil-add-device.md)
- [Команда WDSUTIL Get-Device](wdsutil-get-device.md)
