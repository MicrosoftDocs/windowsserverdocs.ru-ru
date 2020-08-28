---
title: dispdiag
description: Справочная статья по команде диспдиаг, в которой журналы отображают сведения в файле.
ms.topic: reference
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 92dd0b49d8907f3ec934fd59d61b0504b622e80b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030842"
---
# <a name="dispdiag"></a>dispdiag

Журналы отображают сведения в файле.

## <a name="syntax"></a>Синтаксис

```
dispdiag [-testacpi] [-d] [-delay <seconds>] [-out <filepath>]
```

#### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| -тестакпи | Выполняет тестовую диагностику с сочетанием клавиш. Отображает имя ключа, код и код сканирования для любой клавиши, нажатой во время теста. |
| -d | Создает файл дампа с результатами теста. |
| -Delay `<seconds>` | Задерживает сбор данных в указанное время в *секундах*. |
| -out `<filepath>`  | Указывает путь и имя файла для сохранения собранных данных. Это должен быть последний параметр. |
| -? | Отображает доступные параметры команды и предоставляет справку по их использованию. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
