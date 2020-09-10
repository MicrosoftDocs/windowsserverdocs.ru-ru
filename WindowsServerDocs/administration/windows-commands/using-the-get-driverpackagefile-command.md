---
title: Get-Дриверпаккажефиле
description: Справочная статья по Get-Дриверпаккажефиле, в которой отображаются сведения о пакете драйверов, включая драйверы и файлы, которые он содержит.
ms.topic: reference
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9ab52e1040651398d4789ea51ef9b6dc40dc6d54
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624626"
---
# <a name="get-driverpackagefile"></a>Get-Дриверпаккажефиле

Отображает сведения о пакете драйверов, включая драйверы и файлы, которые он содержит.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>Параметры

|         Параметр         |                              Описание                               |
|---------------------------|------------------------------------------------------------------------|
| /Инффиле:\<Inf File path> | Указывает полный путь и имя файла INF-файла пакета драйвера. |
|    [/Арчитектуре: {x86    |                                  ia64                                  |
|     [/Show: {Drivers      |                                 Файлы                                  |

## <a name="examples"></a>Примеры

Чтобы просмотреть сведения о файле драйвера, введите:
```
WDSUTIL /Get-DriverPackageFile /InfFile:C:\temp\1394.inf /Architecture:x86
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)