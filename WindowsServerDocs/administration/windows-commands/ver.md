---
title: ver
description: Справочная статья по версии ver, в которой отображается номер операционной системы.
ms.topic: reference
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1dcbfc9857d23759f919ad01d98b0436b673206e
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636335"
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
