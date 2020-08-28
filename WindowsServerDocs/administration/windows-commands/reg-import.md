---
title: reg import
description: Справочная статья по команде reg import, которая копирует содержимое файла, содержащего экспортированные подразделы, записи и значения реестра, в реестр локального компьютера.
ms.topic: reference
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4da7e3c66bedd3ba6a85e64c69e3fc4866df1e6c
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028042"
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

#### <a name="remarks"></a>Remarks

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
