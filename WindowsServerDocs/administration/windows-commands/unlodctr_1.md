---
title: unlodctr
description: Справочная статья по lodctr, в которой удаляются имена счетчиков производительности и поясняющий текст для службы или драйвера устройства из системного реестра.
ms.topic: article
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3c867a4634024527066c329f408a210e97718d1c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87897043"
---
# <a name="unlodctr"></a>unlodctr

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет имена **счетчиков производительности** и **поясняющий** текст для службы или драйвера устройства из системного реестра.

## <a name="syntax"></a>Синтаксис
```
Unlodctr <DriverName>
```
#### <a name="parameters"></a>Параметры
|Параметр|Описание:|
|-------|--------|
|\<DriverName>|Удаляет параметры имени счетчика производительности и поясняющий текст для драйвера или службы <DriverName> из реестра Windows Server 2003.|
|/?|Отображение справки в командной строке.|

## <a name="remarks"></a>Remarks
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

