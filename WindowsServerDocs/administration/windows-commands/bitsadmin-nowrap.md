---
title: bitsadmin nowrap
description: Справочная статья по команде битсадмин "без переноса", которая усекает любую строку выходного текста, выходящего за пределы крайнего правого края окна командной строки.
ms.topic: reference
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: db66f9e783c3bf3af79cd81fa477cc2f3a9d24e4
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821428"
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
