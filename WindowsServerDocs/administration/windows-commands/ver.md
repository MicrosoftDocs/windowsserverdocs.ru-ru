---
title: ver
description: Справочная статья по версии ver, в которой отображается номер операционной системы.
ms.topic: reference
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 543aceee52be60b6dc90509c326ba1172b2d1ca6
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89023048"
---
# <a name="ver"></a>ver



Отображает номер версии операционной системы.

Эта команда поддерживается в командной строке Windows (Cmd.exe), но не в PowerShell.



## <a name="syntax"></a>Синтаксис

```
ver
```

### <a name="parameters"></a>Параметры

|Параметр|Description|
|---------|-----------|
|/?|Отображение справки в командной строке.|

## <a name="examples"></a>Примеры

Чтобы получить номер версии операционной системы из командной оболочки (cmd.exe), введите:

```
ver
```

Команда ver не работает в PowerShell. Чтобы получить версию ОС из PowerShell, введите:

```powershell
$PSVersionTable.BuildVersion
````


## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
