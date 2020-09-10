---
title: select vdisk
description: Справочная статья для * * * *-
ms.topic: reference
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: daa6d3047e28fb8f6084824fdf1557423daa52b8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639150"
---
# <a name="select-vdisk"></a>select vdisk

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

выбирает указанный виртуальный жесткий диск виртуального жесткого диска \( \) и перемещает фокус на него.

> [!NOTE]
> Эта команда применима только к Windows 7 и Windows Server 2008 R2.

## <a name="syntax"></a>Синтаксис

```
select vdisk file=<full path> [noerr]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|-------|--------|
|File\=<full path>|Указывает полный путь и имя существующего файла виртуального жесткого диска.|
|Noerr|Используется только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки.|

## <a name="examples"></a>Примеры
Чтобы переместить фокус на виртуальный жесткий диск с именем Test. VHD, введите:

```
select vdisk file=c:\test\test.vhd
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

-   [подключить виртуальный диск](attach-vdisk.md)

-   [compact vdisk](compact-vdisk.md)



-   [Отсоединить виртуальный диск](detach-vdisk.md)

-   [detail vdisk](detail-vdisk.md)

-   [expand vdisk](expand-vdisk.md)

-   [Слияние VDISK](merge-vdisk.md)

-   [list_1](./list.md)