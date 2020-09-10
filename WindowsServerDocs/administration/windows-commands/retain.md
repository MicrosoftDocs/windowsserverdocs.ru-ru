---
title: retain
description: Справочная статья по команде "хранить", которая готовит существующий динамический том к использованию в качестве загрузочного или системного тома.
ms.topic: reference
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 201aa8b79f8ac0f89d44be7db3f84c9f3059e206
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626908"
---
# <a name="retain"></a>retain

Подготавливает существующий простой динамический том для использования в качестве загрузочного или системного тома. Если используется динамический диск основной загрузочной записи (MBR), эта команда создает запись раздела в основной загрузочной записи. Если используется динамический диск с таблицей разделов GPT, эта команда создает запись секции в таблице разделов GUID.

## <a name="syntax"></a>Синтаксис

```
retain
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
