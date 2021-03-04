---
title: select vdisk
description: Справочная статья по команде Select vdisk, которая выбирает указанный виртуальный жесткий диск (VHD) и перемещает фокус на него.
ms.topic: reference
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: db876e7492449e40c68756dd5701ad6f4ba629b7
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806087"
---
# <a name="select-vdisk"></a>select vdisk

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Выбирает указанный виртуальный жесткий диск виртуального жесткого диска \( \) и перемещает фокус на него.

## <a name="syntax"></a>Синтаксис

```
select vdisk file=<full path> [noerr]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| файл =`<full path>` | Указывает полный путь и имя существующего файла виртуального жесткого диска. |
| Noerr | Используется только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

## <a name="examples"></a>Примеры

Чтобы переместить фокус на виртуальный жесткий диск с именем *к:\тест\тест.Вхд*, введите:

```
select vdisk file=c:\test\test.vhd
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [подключить виртуальный диск](attach-vdisk.md)

- [compact vdisk](compact-vdisk.md)

- [detach vdisk](detach-vdisk.md)

- [detail vdisk](detail-vdisk.md)

- [expand vdisk](expand-vdisk.md)

- [merge vdisk](merge-vdisk.md)

- [list](list.md)

- [Команда "выбрать диск"](select-disk.md)

- [Команда "выбрать секцию"](select-partition.md)

- [Команда "выбрать том"](select-volume.md)