---
title: Add-Дриверпаккаже
description: Справочная статья по Add-Дриверпаккаже, которая добавляет пакет драйверов на сервер.
ms.topic: reference
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a1876727d4d79cf4ce3c86c654a9be0b7c6795d
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029852"
---
# <a name="add-driverpackage"></a>Add-Дриверпаккаже

Добавляет пакет драйверов на сервер.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL /Add-DriverPackage /InfFile:<Inf File path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>] [/Name:<Friendly Name>]
```

### <a name="parameters"></a>Параметры

|          Параметр           |                                                              Описание                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|   Инффиле:\<Inf File path>   |                                           Указывает полный путь к добавляемому INF-файлу.                                            |
|    Сервером\<Server name>    | Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
|      /Арчитектуре: {x86      |                                                                 ia64                                                                  |
| [/Дриверграуп: \<Group Name> ] |                             Указывает имя группы драйверов, в которую должен быть добавлен пакет.                              |
|   [/Name: \<Friendly Name> ]   |                                           Указывает понятное имя для пакета драйверов.                                            |

## <a name="examples"></a>Примеры

Чтобы добавить пакет драйвера, введите один из следующих элементов:
```
WDSUTIL /verbose /Add-DriverPackage /InfFile:C:\Temp\Display.inf
```
```
WDSUTIL /Add-DriverPackage /Server:MyWDSServer /InfFile:C:\Temp\Display.inf /Architecture:x86 /DriverGroup:x86Drivers /Name:Display Driver
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

