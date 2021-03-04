---
title: serverweroptin
description: Справочная статья по команде сервервероптин, которая позволяет включить отчеты об ошибках.
ms.topic: reference
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d45c8376a31b1554499b89fae0c64af45e6cb629
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805937"
---
# <a name="serverweroptin"></a>serverweroptin

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Позволяет включить отчеты об ошибках.

## <a name="syntax"></a>Синтаксис

```
serverweroptin [/query] [/detailed] [/summary]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /Query | Проверяет текущее значение параметра. |
| /детаилед | Задает автоматическую отправку подробных отчетов. |
| /Summary | Задает автоматическую отправку сводных отчетов. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы проверить текущее значение параметра, введите:

```
serverweroptin /query
```

Чтобы автоматически отправить подробные отчеты, введите:

```
serverweroptin /detailed
```

Чтобы автоматически отправить сводные отчеты, введите:

```
serverweroptin /summary
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
