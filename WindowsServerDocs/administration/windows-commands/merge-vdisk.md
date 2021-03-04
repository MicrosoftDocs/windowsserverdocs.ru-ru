---
title: merge vdisk
description: Справочная статья по команде merge vdisk, которая объединяет разностный виртуальный жесткий диск (VHD) с соответствующим родительским VHD.
ms.topic: reference
ms.assetid: 5865bb08-89a3-406c-8328-0ef8868d03e8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ad858edc440d64a2275411ce43c02c481462518d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101812335"
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
