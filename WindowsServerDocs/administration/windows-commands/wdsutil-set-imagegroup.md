---
title: WDSUTIL Set-имажеграуп
description: Справочная статья по подкоманде Set-Имажеграуп, которая изменяет атрибуты группы образов.
ms.topic: reference
ms.assetid: 4d86946a-e261-4d41-8b0c-1ab0ba2e3430
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e10bd9014b8faa57562b158dee784b01beef1de8
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825078"
---
# <a name="wdsutil-set-imagegroup"></a>WDSUTIL Set-имажеграуп

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет атрибуты группы образов.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /set-imagegroup:<Image group name> [/Server:<Server name>] [/Name:<New image group name>] [/Security:<SDDL>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|/Сет-имажеграуп:<Image group name>|Указывает имя группы образов.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если не указано, будет использоваться локальный сервер.|
|[/Name: <New image group name> ]|Указывает новое имя группы образов.|
|[/Секурити: <SDDL> ]|Указывает новый дескриптор безопасности группы образов в формате языка определения дескрипторов безопасности (SDDL).|
## <a name="examples"></a>Примеры
Чтобы задать имя для группы образов, введите:
```
wdsutil /Set-ImageGroup:ImageGroup1 /Name:New Image Group Name
```
Чтобы указать различные параметры для группы образов, введите:
```
wdsutil /verbose /Set-ImageGroupGroup:ImageGroup1 /Server:MyWDSServer /Name:New Image Group Name
/Security:O:BAG:S-1-5-21-2176941838-3499754553-4071289181-513 D:AI(A;ID;FA;;;SY)(A;OICIIOID;GA;;;SY)(A;ID;FA;;;BA)(A;OICIIOID;GA;;;BA) (A;ID;0x1200a9;;;AU)(A;OICIIOID;GXGR;;;AU)
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Add-имажеграуп](wdsutil-add-imagegroup.md)
- [Команда WDSUTIL Get-аллимажеграупс](wdsutil-get-allimagegroups.md)
- [Команда WDSUTIL Get-имажеграуп](wdsutil-get-imagegroup.md)
- [Команда WDSUTIL Remove-имажеграуп](wdsutil-remove-imagegroup.md)
