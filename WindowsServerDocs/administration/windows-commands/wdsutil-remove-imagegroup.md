---
title: WDSUTIL Remove-имажеграуп
description: Справочная статья по WDSUTIL Remove-имажеграуп, которая удаляет группу образов с сервера.
ms.topic: reference
ms.assetid: 5b2c9813-5df2-4272-8449-26f3bb16f82b
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c775d732b7b8b4f7670c4f3ccb921b4fb30379ed
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825491"
---
# <a name="wdsutil-remove-imagegroup"></a>WDSUTIL Remove-имажеграуп

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет группу образов с сервера.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /remove-ImageGroup Group:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|имажеграуп:<Image group name>|Указывает имя удаляемой группы образов|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
## <a name="examples"></a>Примеры
Чтобы удалить группу образов, введите одно из следующих действий.
```
wdsutil /remove-ImageGroumediaGroup:ImageGroup1
wdsutil /verbose /remove-ImageGroumediaGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Add-имажеграуп](wdsutil-add-imagegroup.md)
- [Команда WDSUTIL Get-аллимажеграупс](wdsutil-get-allimagegroups.md)
- [Команда WDSUTIL Get-имажеграуп](wdsutil-get-imagegroup.md)
- [Команда WDSUTIL Set-имажеграуп](wdsutil-set-imagegroup.md)
