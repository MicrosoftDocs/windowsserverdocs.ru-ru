---
title: compact vdisk
description: Справочная статья по команде Compact vdisk, которая сокращает физический размер динамически расширяемого файла виртуального жесткого диска (VHD).
ms.topic: reference
ms.assetid: 40ca0820-67de-4160-b62a-e9bf63fe2790
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 31d1c11c9ed8b015b8a262227fe1e3a0d9ffe5e3
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101819618"
---
# <a name="compact-vdisk"></a>compact vdisk

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Уменьшает физический размер динамически расширяемого файла виртуального жесткого диска (VHD). Этот параметр полезен, так как при добавлении файлов динамически расширяемые виртуальные жесткие диски увеличиваются в размере, но при удалении файлов автоматическое уменьшение размера не уменьшается.

## <a name="syntax"></a>Синтаксис

```
compact vdisk
```

### <a name="remarks"></a>Remarks

- Для выполнения этой операции необходимо выбрать динамически расширяемый виртуальный жесткий диск. Используйте [команду SELECT VDISK](select-vdisk.md) , чтобы выбрать виртуальный жесткий диск и переместить фокус на него.

- Можно использовать только Compact динамически расширяемые виртуальные жесткие диски, которые отсоединяются или присоединяются как доступные только для чтения.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Attach vdisk](attach-vdisk.md)

- [Команда Detail VDISK](detail-vdisk.md)

- [Команда отсоединения VDISK](detach-vdisk.md)

- [Команда Expand VDISK](expand-vdisk.md)

- [Команда merge VDISK](merge-vdisk.md)

- [команда SELECT VDISK](select-vdisk.md)

- [Команда list](list.md)
