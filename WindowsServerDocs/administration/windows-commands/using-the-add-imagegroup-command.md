---
title: Add-Имажеграуп
description: Справочная статья по Add-Имажеграуп, которая добавляет группу образов на сервер служб развертывания Windows.
ms.topic: reference
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4ee2af4677854e3a4abc727d399ce5a52244aaee
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029762"
---
# <a name="add-imagegroup"></a>Add-Имажеграуп

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет группу образов на сервер служб развертывания Windows.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /add-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
Медиаграуп:<Image group name>|Указывает имя добавляемой группы образов.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
## <a name="examples"></a>Примеры
Чтобы добавить группу образов, введите одно из следующих действий.
```
wdsutil /add-ImageGroumediaGroup:ImageGroup2
wdsutil /verbose /add-ImageGroumediaGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-get-allimagegroups-command.md) 
 Get-аллимажеграупс [Использование команды](using-the-get-imagegroup-command.md) 
 Get-имажеграуп [Использование команды](using-the-remove-imagegroup-command.md) 
 Remove-имажеграуп [Подкоманда: Set-имажеграуп](subcommand-set-imagegroup.md)
