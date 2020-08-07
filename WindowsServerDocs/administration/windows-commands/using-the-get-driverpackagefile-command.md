---
title: Get-Дриверпаккажефиле
description: Справочная статья по Get-Дриверпаккажефиле, в которой отображаются сведения о пакете драйверов, включая драйверы и файлы, которые он содержит.
ms.topic: article
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c80267f90608dca36ef9460eb23b66689022517
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879751"
---
# <a name="get-driverpackagefile"></a>Get-Дриверпаккажефиле

Отображает сведения о пакете драйверов, включая драйверы и файлы, которые он содержит.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>Параметры

|         Параметр         |                              Описание:                               |
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