---
title: WDSUTIL Add-имажеграуп
description: Справочная статья по команде WDSUTIL Add-имажеграуп, которая добавляет группу образов на сервер служб развертывания Windows.
ms.topic: reference
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7c7ad22ac67e0fdbdea50ea642eaafba167f20bb
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804047"
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
