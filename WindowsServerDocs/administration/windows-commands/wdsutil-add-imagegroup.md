---
title: WDSUTIL Add-имажеграуп
description: Справочная статья по команде WDSUTIL Add-имажеграуп, которая добавляет группу образов на сервер служб развертывания Windows.
ms.topic: reference
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3bffb562ba019bb55c783541b78c906dd4a08dc7
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524469"
---
# <a name="wdsutil-add-imagegroup"></a>WDSUTIL Add-имажеграуп

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет группу образов на сервер служб развертывания Windows.

## <a name="syntax"></a>Синтаксис

```
wdsutil [Options] /add-ImageGroup imageGroup:<Imagegroupname> [/Server:<Server name>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| Имажеграуп: `<Imagegroupname>` ] | Указывает имя добавляемого образа. |
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер. |

## <a name="examples"></a>Примеры

Чтобы добавить группу образов, введите:

```
wdsutil /add-ImageGroup imageGroup:ImageGroup2
```

```
wdsutil /verbose /add-Imagegroup imageGroup:My Image Group /Server:MyWDSServer
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Get-аллимажеграупс](wdsutil-get-allimagegroups.md)

- [Команда WDSUTIL Get-имажеграуп](wdsutil-get-imagegroup.md)

- [Команда WDSUTIL Remove-имажеграуп](wdsutil-remove-imagegroup.md)

- [Команда WDSUTIL Set-имажеграуп](wdsutil-set-imagegroup.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
