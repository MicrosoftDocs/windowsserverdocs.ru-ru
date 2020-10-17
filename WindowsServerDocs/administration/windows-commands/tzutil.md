---
title: tzutil
description: Справочная статья по команде tzutil, которая отображает служебную программу часового пояса Windows.
ms.topic: reference
ms.assetid: bcf6e007-c9b6-4df5-83c5-ed7b4b1b5913
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8778758c2e3b72827a7dba5844539d27519a19da
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156339"
---
# <a name="tzutil"></a>tzutil

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает служебную программу часового пояса Windows.

## <a name="syntax"></a>Синтаксис

```
tzutil [/?] [/g] [/s <timezoneID>[_dstoff]] [/l]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /g | Отображает текущий идентификатор часового пояса. |
| ключ `<timezoneID>[_dstoff]` | Задает текущий часовой пояс, используя указанный идентификатор часового пояса. Суффикс **_dstoff** отключает корректировки перехода на летнее время для часового пояса (если применимо). Значение должно быть заключено в кавычки. |
| /l | Список всех допустимых идентификаторов часовых поясов и отображаемых имен. Выходные данные отображаются как:<ul><li>`<display name>`</li><li>`<time zone ID>`</li></ul> |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

Код выхода **0** указывает, что команда выполнена успешно.

## <a name="examples"></a>Примеры

Чтобы отобразить текущий идентификатор часового пояса, введите:

```
tzutil /g
```

Чтобы задать для текущего часового пояса стандартное тихоокеанское время, введите:

```
tzutil /s "Pacific Standard time"
```

Чтобы задать для текущего часового пояса стандартное тихоокеанское время и отключить настройку перехода на летнее время, введите:

```
tzutil /s "Pacific Standard time_dstoff"
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
