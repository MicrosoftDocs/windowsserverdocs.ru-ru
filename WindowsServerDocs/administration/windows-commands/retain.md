---
title: retain
description: Справочная статья по команде "хранить", которая готовит существующий динамический том к использованию в качестве загрузочного или системного тома.
ms.topic: reference
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 17ecb4dea256184d0711662f966dc798ea40b644
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806867"
---
# <a name="retain"></a>retain

Подготавливает существующий простой динамический том для использования в качестве загрузочного или системного тома. Если используется динамический диск основной загрузочной записи (MBR), эта команда создает запись раздела в основной загрузочной записи. Если используется динамический диск с таблицей разделов GPT, эта команда создает запись секции в таблице разделов GUID.

## <a name="syntax"></a>Синтаксис

```
retain
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
