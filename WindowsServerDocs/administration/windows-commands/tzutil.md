---
title: tzutil
description: Справочная статья по команде tzutil, которая отображает служебную программу часового пояса Windows.
ms.topic: reference
ms.assetid: bcf6e007-c9b6-4df5-83c5-ed7b4b1b5913
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5fa7a68dad772abb5bbf35003da7081ac337db13
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804737"
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
