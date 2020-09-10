---
title: Набор подкоманд-Имажеграуп
description: Справочная статья по подкоманде Set-Имажеграуп, которая изменяет атрибуты группы образов.
ms.topic: reference
ms.assetid: 4d86946a-e261-4d41-8b0c-1ab0ba2e3430
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 19a4ed7b8dff69a6fdba5d97e6c9c56e44fe4a06
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640843"
---
# <a name="subcommand-set-imagegroup"></a>Подкоманда: Set-Имажеграуп

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет атрибуты группы образов.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Set-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/Name:<New image group name>] [/Security:<SDDL>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
Медиаграуп:<Image group name>|Указывает имя группы образов.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если не указано, будет использоваться локальный сервер.|
|[/Name: <New image group name> ]|Указывает новое имя группы образов.|
|[/Секурити: <SDDL> ]|Указывает новый дескриптор безопасности группы образов в формате языка определения дескрипторов безопасности (SDDL).|
## <a name="examples"></a>Примеры
Чтобы задать имя для группы образов, введите:
```
wdsutil /Set-ImageGroumediaGroup:ImageGroup1 /Name:New Image Group Name
```
Чтобы указать различные параметры для группы образов, введите:
```
wdsutil /verbose /Set-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /Name:New Image Group Name
/Security:O:BAG:S-1-5-21-2176941838-3499754553-4071289181-513 D:AI(A;ID;FA;;;SY)(A;OICIIOID;GA;;;SY)(A;ID;FA;;;BA)(A;OICIIOID;GA;;;BA) (A;ID;0x1200a9;;;AU)(A;OICIIOID;GXGR;;;AU)
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-add-imagegroup-command.md) 
 Add-имажеграуп [Использование команды](using-the-get-allimagegroups-command.md) 
 Get-аллимажеграупс [Использование команды](using-the-get-imagegroup-command.md) 
 Get-имажеграуп [Использование команды Remove-имажеграуп](using-the-remove-imagegroup-command.md)
