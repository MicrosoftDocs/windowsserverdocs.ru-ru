---
title: WDSUTIL Get-дриверпаккажефиле
description: Справочная статья по WDSUTIL Get-дриверпаккажефиле, в которой отображаются сведения о пакете драйверов, включая драйверы и файлы, которые он содержит.
ms.topic: reference
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f85d57a81aa63f6ecb94b4b09a1614403aa19664
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730836"
---
# <a name="wdsutil-get-driverpackagefile"></a>WDSUTIL Get-дриверпаккажефиле

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