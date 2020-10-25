---
title: WDSUTIL Add-аллдриверпаккажес
description: Справочная статья по команде WDSUTIL Add-аллдриверпаккажес, которая добавляет все пакеты драйверов, хранящиеся в папке, на сервер.
ms.topic: reference
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 07d958fb382f040db34f486a28fed4b924ce45d8
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524659"
---
# <a name="wdsutil-add-alldriverpackages"></a>WDSUTIL Add-аллдриверпаккажес

Добавляет все пакеты драйверов, хранящиеся в папке, на сервер.

## <a name="syntax"></a>Синтаксис

```
wdsutil /Add-AllDriverPackages /FolderPath:<folderpath> [/Server:<servername>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<groupname>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| FolderPath`<folderpath>` | Указывает полный путь к папке, содержащей INF-файлы для пакетов драйверов. |
| [/Server: `<servername>` ] | Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
| [/Арчитектуре: `{x86|ia64|x64}` ] | Указывает тип архитектуры для пакета драйверов. |
| [/Дриверграуп: `<groupname>` ] | Указывает имя группы драйверов, в которую должны быть добавлены пакеты. |

## <a name="examples"></a>Примеры

Чтобы добавить пакеты драйверов, введите:

```
wdsutil /verbose /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers /Architecture:x86
```

```
wdsutil /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers\Printers /DriverGroup:Printer Drivers
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)

- [Add-Вдсдриверпаккаже](/powershell/module/wds/add-wdsdriverpackage)
