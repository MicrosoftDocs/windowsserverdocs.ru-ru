---
title: unlodctr
description: Справочная статья по команде lodctr, которая удаляет имена счетчиков производительности и поясняющий текст для службы или драйвера устройства из системного реестра.
ms.topic: reference
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a57a8ffa143c73970ff82ec2c5894678e3829fd3
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804727"
---
# <a name="unlodctr"></a>unlodctr

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет **имена счетчиков производительности** и **поясняющий текст** для службы или драйвера устройства из системного реестра.

> [!WARNING]
> Неправильное изменение реестра может серьезно повредить систему. Перед внесением изменений следует сделать резервную копию всех ценных данных на компьютере.

## <a name="syntax"></a>Синтаксис

```
unlodctr <drivername>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<drivername>` | Удаляет параметры **имени счетчика производительности** и **поясняющий текст** для драйвера или службы `<drivername>` из реестра Windows Server. Если в `<drivername>` число включаемых пробелов, необходимо использовать кавычки для текста, например "имя драйвера". |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы удалить текущие **имена счетчиков производительности** и **поясняющий текст** для службы SMTP, введите:

```
unlodctr SMTPSVC
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
