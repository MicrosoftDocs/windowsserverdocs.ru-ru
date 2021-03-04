---
title: Add-Дриверпаккаже
description: Справочная статья по команде Add-Дриверпаккаже, которая добавляет пакет драйверов на сервер.
ms.topic: reference
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d1cb060eebe973db099f9d26812ce9e3e1d33d83
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804137"
---
# <a name="add-driverpackage"></a>Add-Дриверпаккаже

Добавляет пакет драйверов на сервер.

## <a name="syntax"></a>Синтаксис

```
wdsutil /Add-DriverPackage /InfFile:<Inf File path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>] [/Name:<Friendly Name>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /Инффиле:`<InfFilepath>` | Указывает полный путь к добавляемому INF-файлу. |
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
| [/Арчитектуре: `{x86 | ia64 | x64}` ] | Указывает тип архитектуры для пакета драйверов. |
| [/Дриверграуп: `<groupname>` ] | Указывает имя группы драйверов, в которую должны быть добавлены пакеты. |
| [/Name: `<friendlyname>` ] | Указывает понятное имя для пакета драйверов. |

## <a name="examples"></a>Примеры

Чтобы добавить пакет драйвера, введите:

```
wdsutil /verbose /Add-DriverPackage /InfFile:C:\Temp\Display.inf
```

```
wdsutil /Add-DriverPackage /Server:MyWDSServer /InfFile:C:\Temp\Display.inf /Architecture:x86 /DriverGroup:x86Drivers /Name:Display Driver
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Add-дриверграуппаккаже](wdsutil-add-drivergrouppackage.md)

- [Команда WDSUTIL Add-аллдриверпаккажес](wdsutil-add-alldriverpackages.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
