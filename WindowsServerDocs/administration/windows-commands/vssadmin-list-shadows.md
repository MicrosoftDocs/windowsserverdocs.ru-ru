---
title: vssadmin list shadows
description: Описание команды vssadmin List Shadows, в которой перечислены все существующие теневые копии указанного тома.
ms.topic: reference
author: JasonGerend
ms.author: jgerend
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: cb7ddaa09e2da350c1c5422c6224aabd8831f763
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156208"
---
# <a name="vssadmin-list-shadows"></a>vssadmin list shadows

> Область применения: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Список всех существующих теневых копий указанного тома. Если эта команда используется без параметров, она отображает все теневые копии томов на компьютере в порядке, указанном в **наборе теневых копий**.

## <a name="syntax"></a>Синтаксис

```
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /фор =`<ForVolumeSpec>` | Указывает, для какого тома будут перечислены теневые копии. |
| /Шадов =`<ShadowID>` | Выводит список теневых копий, заданных параметром Шадовид. Чтобы получить идентификатор теневой копии, используйте [команду vssadmin List Shadows](vssadmin-list-shadows.md). При вводе идентификатора теневой копии используйте следующий формат, где каждый *X* представляет шестнадцатеричный символ:<p>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [vssadmin, команда](vssadmin.md)

- [Команда VSSadmin list Shadows](vssadmin-list-shadows.md)
