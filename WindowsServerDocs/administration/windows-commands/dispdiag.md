---
title: dispdiag
description: Справочная статья по команде диспдиаг, в которой журналы отображают сведения в файле.
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78b8080395fa30a934d1a9380bf86beae7e62dc0
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890828"
---
# <a name="dispdiag"></a>dispdiag

Журналы отображают сведения в файле.

## <a name="syntax"></a>Синтаксис

```
dispdiag [-testacpi] [-d] [-delay <seconds>] [-out <filepath>]
```

#### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| -тестакпи | Выполняет тестовую диагностику с сочетанием клавиш. Отображает имя ключа, код и код сканирования для любой клавиши, нажатой во время теста. |
| -d | Создает файл дампа с результатами теста. |
| -Delay`<seconds>` | Задерживает сбор данных в указанное время в *секундах*. |
| -out`<filepath>`  | Указывает путь и имя файла для сохранения собранных данных. Это должен быть последний параметр. |
| -? | Отображает доступные параметры команды и предоставляет справку по их использованию. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
