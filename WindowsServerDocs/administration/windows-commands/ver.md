---
title: ver
description: Справочная статья по команде ver, которая отображает номер версии операционной системы.
ms.topic: reference
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1e0d3070d480905d0cbff37892fc1500bc50b172
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804717"
---
# <a name="ver"></a>ver

Отображает номер версии операционной системы. Эта команда поддерживается в командной строке Windows (Cmd.exe), но не в PowerShell.

## <a name="syntax"></a>Синтаксис

```
ver
```

### <a name="parameters"></a>Параметры

| Параметр | Description |
|--|--|
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы получить номер версии операционной системы из командной оболочки (cmd.exe), введите:

```
ver
```

Команда **ver** не работает в PowerShell. Если вы хотите получить номер версии операционной системы с помощью PowerShell, введите:

```powershell
$PSVersionTable.BuildVersion
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
