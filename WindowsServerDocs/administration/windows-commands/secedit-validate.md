---
title: secedit validate
description: Справочная статья по команде secedit Validate, которая проверяет параметры безопасности, хранящиеся в шаблоне безопасности.
ms.topic: reference
ms.assetid: 9fb06354-f55a-4ca4-9fbc-9a872eb9b9cf
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 057573cf5bc28a47f5140fb58e23ee1ed4bbc4c1
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388105"
---
# <a name="secedit-validate"></a>Secedit/Validate

Проверяет параметры безопасности, хранящиеся в шаблоне безопасности (INF-файле). Проверка шаблонов безопасности может помочь определить, поврежден или неправильно задан один из них. Поврежденные или несоответствующие настройки шаблонов безопасности не применяются.

## <a name="syntax"></a>Синтаксис

```
secedit /validate <configuration file name>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<configuration file name>` | Обязательный. Указывает путь и имя файла для шаблона безопасности, который будет проверен. Файлы журнала не обновляются этой командой. |

## <a name="examples"></a>Примеры

Чтобы убедиться, что файл Rollback. inf *секрбкконтосо. INF*все еще действителен после отката, введите:

```
secedit /validate secRBKcontoso.inf
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Secedit/Analyze](secedit-analyze.md)

- [Secedit/configure](secedit-configure.md)

- [Secedit/Export](secedit-export.md)

- [Secedit/женератероллбакк](secedit-generaterollback.md)

- [Secedit/Import](secedit-import.md)