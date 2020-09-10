---
title: reg import
description: Справочная статья по команде reg import, которая копирует содержимое файла, содержащего экспортированные подразделы, записи и значения реестра, в реестр локального компьютера.
ms.topic: reference
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 49f83a20b4f9c9e1e64f6e33f0980757de60d9ec
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627032"
---
# <a name="reg-import"></a>reg import

Копирует содержимое файла, содержащего экспортированные подразделы, записи и значения реестра, в реестр локального компьютера.

## <a name="syntax"></a>Синтаксис

```
reg import <filename>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<filename>` | Указывает имя и путь к файлу, который содержит содержимое, копируемое в реестр локального компьютера. Этот файл должен быть создан заранее с помощью команды **reg export**. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Примечания

- Возвращаемые значения для операции **reg import** :

    | Значение | Описание |
    |--|--|
    | 0 | Успех |
    | 1 | Сбой |

### <a name="examples"></a>Примеры

Чтобы импортировать записи реестра из файла с именем Аппбкуп. reg, введите:

```
reg import AppBkUp.reg
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Reg Export](reg-export.md)
