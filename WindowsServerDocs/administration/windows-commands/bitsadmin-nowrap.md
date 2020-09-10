---
title: bitsadmin nowrap
description: Справочная статья по команде битсадмин "без переноса", которая усекает любую строку выходного текста, выходящего за пределы крайнего правого края окна командной строки.
ms.topic: reference
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2e5724f3dedb808898cd070026e2e4a944d4731b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631425"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

Усекает любую строку выходного текста, выходящую за пределы крайнего правого края окна командной строки. По умолчанию все параметры, кроме коммутатора **монитора** , заключают выходные данные в оболочку. Укажите параметр "не **переносить** " перед другими параметрами.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /nowrap
```

## <a name="examples"></a>Примеры

Чтобы получить состояние для задания с именем *мидовнлоаджоб* , не заключив в оболочку выходные данные:

```
bitsadmin /nowrap /getstate myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
