---
title: merge vdisk
description: Справочная статья по команде merge vdisk, которая объединяет разностный виртуальный жесткий диск (VHD) с соответствующим родительским VHD.
ms.topic: reference
ms.assetid: 5865bb08-89a3-406c-8328-0ef8868d03e8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 99a51b422c0e4bb19be4227b43fba6a5ef430628
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635168"
---
# <a name="merge-vdisk"></a>merge vdisk

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Объединяет разностный виртуальный жесткий диск (VHD) с соответствующим ему родительским VHD. Родительский виртуальный жесткий диск будет изменен для включения изменений из разностного виртуального жесткого диска. Эта команда изменяет родительский виртуальный жесткий диск. В результате другие разностные виртуальные жесткие диски, зависящие от родительского, станут недействительными.

> [!IMPORTANT]
> Для выполнения этой операции необходимо выбрать и отсоединить виртуальный жесткий диск. Используйте команду **SELECT VDISK** , чтобы выбрать виртуальный жесткий диск и переместить фокус на него.

## <a name="syntax"></a>Синтаксис

```
merge vdisk depth=<n>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| Глубина =`<n>` | Указывает число родительских VHD-файлов, объединяемых вместе. Например, `depth=1` указывает, что разностный виртуальный жесткий диск будет объединен с одним уровнем разностной цепочки. |

### <a name="examples"></a>Примеры

Чтобы объединить разностный виртуальный жесткий диск с его родительским VHD, введите:

```
merge vdisk depth=1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Attach vdisk](attach-vdisk.md)

- [Команда Compact VDISK](compact-vdisk.md)

- [Команда Detail VDISK](detail-vdisk.md)

- [Команда отсоединения VDISK](detach-vdisk.md)

- [Команда Expand VDISK](expand-vdisk.md)

- [команда SELECT VDISK](select-vdisk.md)

- [Команда list](list.md)
