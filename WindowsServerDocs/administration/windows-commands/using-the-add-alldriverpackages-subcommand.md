---
title: Использование подкоманды Add-Аллдриверпаккажес
description: Справочная статья по Add-Аллдриверпаккажес, которая добавляет все пакеты драйверов, которые хранятся в папке на сервере.
ms.topic: reference
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ccdd132687fdc65336aeb49d317f9ccf5fbcd968
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89032189"
---
# <a name="add-alldriverpackages"></a>Add-Аллдриверпаккажес

Добавляет все пакеты драйверов, хранящиеся в папке, на сервер.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL /Add-AllDriverPackages /FolderPath:<Folder Path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>]
```

### <a name="parameters"></a>Параметры

|          Параметр           |                                                              Описание                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|  FolderPath\<Folder Path>  |                      Указывает полный путь к папке, содержащей INF-файлы для пакетов драйверов.                      |
|   [/Server: \<Server name> ]   | Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
|     [/Арчитектуре: {x86      |                                                                 ia64                                                                  |
| [/Дриверграуп: \<Group Name> ] |                             Указывает имя группы драйверов, в которую должны быть добавлены пакеты.                             |

## <a name="examples"></a>Примеры

Чтобы добавить пакеты драйверов, введите один из следующих элементов:
```
WDSUTIL /verbose /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers /Architecture:x86
```
```
WDSUTIL /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers\Printers /DriverGroup:Printer Drivers
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

[Add-Вдсдриверпаккаже](/previous-versions/windows/powershell-scripting/dn283440(v=wps.630))
