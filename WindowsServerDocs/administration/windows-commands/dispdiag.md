---
title: dispdiag
description: Справочная статья по команде диспдиаг, в которой журналы отображают сведения в файле.
ms.topic: reference
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d2171aae18601f3783389335ea1cfa592a5c7f23
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627158"
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
