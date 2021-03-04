---
title: expand vdisk
description: Справочная статья по команде Expand vdisk, которая расширяет виртуальный жесткий диск (VHD) до указанного размера.
ms.topic: reference
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d4c245f0e1570e4b9bfaa9509f4bb0a84217bdd6
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101818268"
---
# <a name="expand-vdisk"></a>expand vdisk

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Расширение виртуального жесткого диска (VHD) до указанного размера.

Для выполнения этой операции необходимо выбрать и отсоединить виртуальный жесткий диск. Используйте [команду SELECT VDISK](select-vdisk.md) , чтобы выбрать том и переместить фокус на него.

## <a name="syntax"></a>Синтаксис

```
expand vdisk maximum=<n>
```

### <a name="parameters"></a>Параметры

 | Параметр | Описание |
 |---------- | ----------- |
 | максимум =`<n>` | Указывает новый размер виртуального жесткого диска в мегабайтах (МБ). |

### <a name="examples"></a>Примеры

Чтобы расширить выбранный виртуальный жесткий диск до 20 ГБ, введите:

```
expand vdisk maximum=20000
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда SELECT VDISK](select-vdisk.md)

- [Команда Attach vdisk](attach-vdisk.md)

- [Команда Compact VDISK](compact-vdisk.md)

- [Команда отсоединения VDISK](detach-vdisk.md)

- [Команда Detail VDISK](detail-vdisk.md)

- [Команда merge VDISK](merge-vdisk.md)

- [Команда list](list.md)
