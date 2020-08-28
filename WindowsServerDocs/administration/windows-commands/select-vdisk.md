---
title: select vdisk
description: Справочная статья для * * * *-
ms.topic: reference
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 388804d8b895e636937050c6d04cae02cd30a0e8
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89032317"
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