---
title: logman create
description: Справочная статья по команде Logman Create, которая создает счетчик, трассировку, сборщик данных конфигурации или API.
ms.topic: reference
ms.assetid: 972f0126-7bc4-4b14-9265-062864f3ffd4
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 39b8abfb11c5d5cf5de0c574a02aa72ff363fa88
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101813955"
---
# <a name="logman-create"></a>logman create

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Создает счетчик, трассировку, сборщик данных конфигурации или API.

## <a name="syntax"></a>Синтаксис

```
logman create <counter | trace | alert | cfg | api> <[-n] <name>> [options]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| [logman create counter](logman-create-counter.md) | Создает сборщик данных счетчика. |
| [logman create trace](logman-create-trace.md) | Создает сборщик данных трассировки. |
| [logman create alert](logman-create-alert.md) | Создает сборщик данных предупреждений. |
| [logman create cfg](logman-create-cfg.md) | Создает сборщик данных конфигурации. |
| [logman create api](logman-create-api.md) | Создает сборщик данных трассировки API. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда logman](logman.md)