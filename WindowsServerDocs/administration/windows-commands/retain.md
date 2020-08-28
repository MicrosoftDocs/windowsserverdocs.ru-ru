---
title: retain
description: Справочная статья по команде "хранить", которая готовит существующий динамический том к использованию в качестве загрузочного или системного тома.
ms.topic: reference
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 98c27c62ab7e0ac3320986dde6049be40d10db57
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89036993"
---
# <a name="retain"></a>retain

Подготавливает существующий простой динамический том для использования в качестве загрузочного или системного тома. Если используется динамический диск основной загрузочной записи (MBR), эта команда создает запись раздела в основной загрузочной записи. Если используется динамический диск с таблицей разделов GPT, эта команда создает запись секции в таблице разделов GUID.

## <a name="syntax"></a>Синтаксис

```
retain
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
