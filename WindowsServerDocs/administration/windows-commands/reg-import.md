---
title: reg import
description: Справочная статья по команде reg import, которая копирует содержимое файла, содержащего экспортированные подразделы, записи и значения реестра, в реестр локального компьютера.
ms.topic: reference
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1c218344504e405ef586a58a8193c012b5fd6dd4
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101807307"
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

#### <a name="remarks"></a>Комментарии

- Возвращаемые значения для операции **reg import** :

    | Значение | Описание |
    |--|--|
    | 0 | Успешное завершение |
    | 1 | Сбой |

### <a name="examples"></a>Примеры

Чтобы импортировать записи реестра из файла с именем Аппбкуп. reg, введите:

```
reg import AppBkUp.reg
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Reg Export](reg-export.md)
