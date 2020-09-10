---
title: logman
description: Справочная статья по команде logman, которая создает сеанс трассировки событий и журналы производительности и управляет ими, а также поддерживает многие функции системного монитора из командной строки.
ms.topic: reference
ms.assetid: 574a5203-5b3b-4759-a678-f26d00dde447
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ac3e541436ca6f3b0e9d7c0dc03154ffefdfda0d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639517"
---
# <a name="logman"></a>logman

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Создает и управляет сеансами трассировки событий и журналами производительности, а также поддерживает многие функции системного монитора из командной строки.

## <a name="syntax"></a>Синтаксис

```
logman [create | query | start | stop | delete| update | import | export | /?] [options]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| [logman create](logman-create.md) | Создает счетчик, трассировку, сборщик данных конфигурации или API. |
| [logman query](logman-query.md) | Запрашивает свойства сборщика данных. |
| [logman start &#124; stop](logman-start-stop.md) | Запускает или останавливает сбор данных. |
| [logman delete](logman-delete.md) | Удаляет существующий сборщик данных. |
| [logman update](logman-update.md) | Обновляет свойства существующего сборщика данных. |
| [logman import &#124; export](logman-import-export.md) | Импортирует набор сборщиков данных из XML-файла или экспортирует набор сборщиков данных в XML-файл. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)