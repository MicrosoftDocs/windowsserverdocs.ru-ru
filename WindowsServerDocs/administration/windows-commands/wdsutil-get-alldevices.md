---
title: WDSUTIL Get-аллдевицес
description: Справочная статья по команде WDSUTIL Get-аллдевицес, которая отображает свойства служб развертывания Windows для всех предварительно подготовленных компьютеров.
ms.topic: reference
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 45c93f77dc0a77cdaec3974bfabea069684437ad
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101803759"
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
