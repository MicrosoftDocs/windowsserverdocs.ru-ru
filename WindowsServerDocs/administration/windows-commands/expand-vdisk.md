---
title: expand vdisk
description: Справочная статья по команде Expand vdisk, которая расширяет виртуальный жесткий диск (VHD) до указанного размера.
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5d9c5c859dfa506d9f8afd07a0e78bdef210f60a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890441"
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
