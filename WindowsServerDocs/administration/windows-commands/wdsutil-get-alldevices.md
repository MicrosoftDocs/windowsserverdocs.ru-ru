---
title: WDSUTIL Get-аллдевицес
description: Справочная статья по команде WDSUTIL Get-аллдевицес, которая отображает свойства служб развертывания Windows для всех предварительно подготовленных компьютеров.
ms.topic: reference
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a960a30fd61056e2e2eb183e8a873223daa78be2
ms.sourcegitcommit: 28b5ab74cb0b40539ccc1a83998d6391e87fe51f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2020
ms.locfileid: "96614876"
---
# <a name="wdsutil-get-alldevices"></a>WDSUTIL Get-аллдевицес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает свойства служб развертывания Windows для всех предварительно подготовленных компьютеров. Предварительно подготовленный компьютер — это физический компьютер, связанный с учетной записью компьютера в доменных службах Active Directory.

## <a name="syntax"></a>Синтаксис

```
wdsutil [options] /get-alldevices [/forest:{Yes | No}] [/referralserver:<servername>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `[/forest:{Yes | No}]` | Указывает, должны ли службы развертывания Windows возвращать компьютеры во всем лесу или в локальном домене. Значение по умолчанию — « **нет**». Это означает, что возвращаются только компьютеры в локальном домене. |
| `[/referralserver:<servername>]` | Возвращает только те компьютеры, которые предварительно подготовлены для указанного сервера. |

## <a name="examples"></a>Примеры

Чтобы просмотреть все компьютеры, введите:

```
wdsutil /get-alldevices
```

```
wdsutil /verbose /get-alldevices /forest:Yes /referralserver:MyWDSServer
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Set-Device](wdsutil-set-device.md)

- [Команда WDSUTIL Add-Device](wdsutil-add-device.md)

- [Команда WDSUTIL Get-Device](wdsutil-get-device.md)
