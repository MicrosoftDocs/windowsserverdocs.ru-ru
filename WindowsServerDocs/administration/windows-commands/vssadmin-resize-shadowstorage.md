---
title: Vssadmin изменение размера шадовстораже
description: Описание команды vssadmin Resize шадовстораже.
ms.topic: reference
author: JasonGerend
ms.author: jgerend
ms.date: 03/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0eb9a4096c529b73a87c5a9fb4d6a95b5e655fe3
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89022838"
---
# <a name="vssadmin-resize-shadowstorage"></a>Vssadmin изменение размера шадовстораже

> Область применения: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Изменяет максимальный объем дискового пространства, который можно использовать для хранения теневых копий.

Минимальный объем дискового пространства, который можно использовать для хранения теневых копий, можно указать с помощью значения реестра **миндиффареафилесизе** . Дополнительные сведения см. в разделе [миндиффареафилесизе](/windows/win32/backup/registry-keys-for-backup-and-restore#mindiffareafilesize).

> [!WARNING]
> Изменение размера связи хранилища может привести к исчезновению теневых копий.

## <a name="syntax"></a>Синтаксис

```cmd
vssadmin resize shadowstorage /for=<ForVolumeSpec> /on=<OnVolumeSpec> [/maxsize=<MaxSizeSpec>]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---|---|
`/for=<ForVolumeSpec>`  | Указывает том, для которого необходимо изменить размер пространства в хранилище.
`/on=<OnVolumeSpec>` | Указывает том хранилища.
`[/maxsize=<MaxSizeSpec>]` |  Указывает максимальный объем пространства, который может использоваться для хранения теневых копий. Если для/макссизе не указано значение, ограничение на объем хранилища, которое можно использовать, не ограничено.  <br> <br> Значение Макссизеспек должно быть не меньше 1 МБ и должно быть выражено в одном из следующих единиц: КБ, МБ, ГБ, ТБ, PB или EB. Если единица не указана, Макссизеспек использует байты по умолчанию.

## <a name="examples"></a>Примеры

```cmd
vssadmin Resize ShadowStorage /For=C: /On=D: /MaxSize=900MB
vssadmin Resize ShadowStorage /For=C: /On=D: /MaxSize=UNBOUNDED
vssadmin Resize ShadowStorage /For=C: /On=C: /MaxSize=20%
```

## <a name="additional-references"></a>Дополнительные ссылки

* [Ключ синтаксиса командной строки](./command-line-syntax-key.md)
* [List](vssadmin.md)
