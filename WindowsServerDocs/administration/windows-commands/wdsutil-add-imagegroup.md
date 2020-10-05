---
title: WDSUTIL Add-имажеграуп
description: Справочная статья по WDSUTIL Add-имажеграуп, которая добавляет группу образов на сервер служб развертывания Windows.
ms.topic: reference
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 97f1439a4212a770dff6f6c42837c531f08c3d25
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91731052"
---
# <a name="wdsutil-add-imagegroup"></a>WDSUTIL Add-имажеграуп

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет группу образов на сервер служб развертывания Windows.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /add-ImageGroup imageGroup:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|имажеграуп:<Image group name>|Указывает имя добавляемой группы образов.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
## <a name="examples"></a>Примеры
Чтобы добавить группу образов, введите одно из следующих действий.
```
wdsutil /add-ImageGroup imageGroup:ImageGroup2
wdsutil /verbose /add-Imagegroup imageGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Get-аллимажеграупс](wdsutil-get-allimagegroups.md)
- [Команда WDSUTIL Get-имажеграуп](wdsutil-get-imagegroup.md)
- [Команда WDSUTIL Remove-имажеграуп](wdsutil-remove-imagegroup.md)
- [Команда WDSUTIL Set-имажеграуп](wdsutil-set-imagegroup.md)
