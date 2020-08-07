---
title: tzutil
description: Справочная статья по tzutil, в которой отображается служебная программа часового пояса Windows.
ms.topic: article
ms.assetid: bcf6e007-c9b6-4df5-83c5-ed7b4b1b5913
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4727423ed6752b3a0c2b578f5838a1108d1d14d4
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896634"
---
# <a name="tzutil"></a>tzutil

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает служебную программу часового пояса Windows.

## <a name="syntax"></a>Синтаксис
```
tzutil [/?] [/g] [/s <timeZoneID>[_dstoff]] [/l]
```
#### <a name="parameters"></a>Параметры
|Параметр|Description|
|-------|--------|
|/?|Отображение справки в командной строке.|
|/g|Отображает текущий идентификатор часового пояса.|
|/s \<timeZoneID> [_dstoff]|Задает текущий часовой пояс, используя указанный идентификатор часового пояса. Суффикс **_dstoff** отключает корректировки перехода на летнее время для часового пояса (если применимо).|
|/l|Список всех допустимых идентификаторов часовых поясов и отображаемых имен. Выходные данные должны выглядеть следующим образом:<p>-   \<display name><br />-   \<time zone ID>|

## <a name="remarks"></a>Remarks
Код выхода **0** указывает, что команда выполнена успешно.

## <a name="examples"></a>Примеры
Чтобы отобразить текущий идентификатор часового пояса, введите:
```
tzutil /g
```
Чтобы задать для текущего часового пояса стандартное тихоокеанское время, введите:
```
tzutil /s Pacific Standard time
```
Чтобы задать для текущего часового пояса стандартное тихоокеанское время и отключить настройку перехода на летнее время, введите:
```
tzutil /s Pacific Standard time_dstoff
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

