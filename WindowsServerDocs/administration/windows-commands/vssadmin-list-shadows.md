---
title: Vssadmin List Shadows
description: Описание команды vssadmin List Shadows.
ms.topic: reference
author: JasonGerend
ms.author: jgerend
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: ee35fd65a6fdab68b8f4e4155d52182980b2d0c9
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89022911"
---
# <a name="vssadmin-list-shadows"></a>Vssadmin List Shadows

> Область применения: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Список всех существующих теневых копий указанного тома. Если эта команда используется без параметров, она отображает все теневые копии томов на компьютере в порядке, указанном в **наборе теневых копий**.

## <a name="syntax"></a>Синтаксис

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---|---|
|/фор =\<ForVolumeSpec>|Указывает, для какого тома будут перечислены теневые копии.|
|/Шадов =\<ShadowID>|Выводит список теневых копий, заданных параметром Шадовид. Чтобы получить идентификатор теневой копии, используйте команду **vssadmin List Shadows** . При вводе идентификатора теневой копии используйте следующий формат, где каждый *X* представляет шестнадцатеричный символ:<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|

## <a name="additional-references"></a>Дополнительные ссылки

* [Ключ синтаксиса командной строки](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [List](vssadmin.md)
