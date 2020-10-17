---
title: vssadmin resize shadowstorage
description: Описание команды vssadmin Resize шадовстораже, которая изменяет максимальный объем пространства в хранилище, который может использоваться для хранения теневых копий.
ms.topic: reference
author: JasonGerend
ms.author: jgerend
ms.date: 03/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 704130890d68c271e74a9163ba4ae76dcfb1a516
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156148"
---
# <a name="vssadmin-resize-shadowstorage"></a>vssadmin resize shadowstorage

> Область применения: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Изменяет максимальный объем дискового пространства, который можно использовать для хранения теневых копий.

Минимальный объем дискового пространства, который можно использовать для хранения теневых копий, можно указать с помощью значения реестра **миндиффареафилесизе** . Дополнительные сведения см. в разделе [миндиффареафилесизе](/windows/win32/backup/registry-keys-for-backup-and-restore#mindiffareafilesize).

> [!WARNING]
> Изменение размера связи хранилища может привести к исчезновению теневых копий.

## <a name="syntax"></a>Синтаксис

```
vssadmin resize shadowstorage /for=<ForVolumeSpec> /on=<OnVolumeSpec> [/maxsize=<MaxSizeSpec>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /фор =`<ForVolumeSpec>` | Указывает том, для которого необходимо изменить размер пространства в хранилище. |
| /on =`<OnVolumeSpec>` | Указывает том хранилища. |
| [/макссизе = `<MaxSizeSpec>` ] | Указывает максимальный объем пространства, который может использоваться для хранения теневых копий. Если для **/макссизе**не указано значение, то ограничения на объем хранилища, который можно использовать, не накладываются.<p>Значение **макссизеспек** должно быть не меньше 1 МБ и должно быть выражено в одном из следующих единиц: КБ, МБ, ГБ, ТБ, Pb или EB. Если единица не указана, **макссизеспек** использует байты по умолчанию. |

## <a name="examples"></a>Примеры

Чтобы изменить размер теневой копии тома C на томе D с максимальным размером 900MB, введите:

```
vssadmin resize shadowstorage /For=C: /On=D: /MaxSize=900MB
```

Чтобы изменить размер теневой копии тома C на томе D без максимального размера, введите:

```
vssadmin resize shadowstorage /For=C: /On=D: /MaxSize=UNBOUNDED
```

Чтобы изменить размер теневой копии тома C на 20%, введите:

```
vssadmin resize shadowstorage /For=C: /On=C: /MaxSize=20%
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [vssadmin, команда](vssadmin.md)
