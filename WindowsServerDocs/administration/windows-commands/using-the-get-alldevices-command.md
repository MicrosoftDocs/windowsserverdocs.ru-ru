---
title: Get-Аллдевицес
description: Справочная статья по Get-Аллдевицес, в которой отображаются свойства служб развертывания Windows для всех предварительно подготовленных компьютеров.
ms.topic: article
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1e527be333570838ecb675d78742bbf55918eff3
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896979"
---
# <a name="get-alldevices"></a>Get-Аллдевицес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает свойства служб развертывания Windows для всех предварительно подготовленных компьютеров. Предварительно подготовленный компьютер — это физический компьютер, связанный с учетной записью компьютера в доменных службах Active Directory.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Get-AllDevices [/forest:{Yes | No}] [/ReferralServer:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание:|
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
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Подкоманда: Set-Device](subcommand-set-device.md) 
 [Использование команды](using-the-add-device-command.md) 
 Add-Device [Использование команды Get-Device](using-the-get-device-command.md)
