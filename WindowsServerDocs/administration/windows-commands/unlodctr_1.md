---
title: unlodctr
description: Справочная статья по lodctr, в которой удаляются имена счетчиков производительности и поясняющий текст для службы или драйвера устройства из системного реестра.
ms.topic: reference
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e0494d0b4509c4b75af9ca8473e3ae65353e02c1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626564"
---
# <a name="unlodctr"></a>unlodctr

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет имена **счетчиков производительности** и **поясняющий** текст для службы или драйвера устройства из системного реестра.

## <a name="syntax"></a>Синтаксис
```
Unlodctr <DriverName>
```
#### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|\<DriverName>|Удаляет параметры имени счетчика производительности и поясняющий текст для драйвера или службы <DriverName> из реестра Windows Server 2003.|
|/?|Отображение справки в командной строке.|

## <a name="remarks"></a>Примечания
> [!WARNING]
> Неправильное изменение реестра может серьезно повредить систему. Перед внесением изменений следует сделать резервную копию всех ценных данных на компьютере.

Если предоставленные сведения содержат пробелы, заключите текст в кавычки (например, <DriverName> ).

## <a name="examples"></a>Примеры
Чтобы удалить текущие параметры реестра производительности и текст объяснения счетчика для службы SMTP:
```
unlodctr SMTPSVC
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

