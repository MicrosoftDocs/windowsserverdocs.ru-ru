---
title: title
description: Справочная статья по команде Title, которая создает заголовок для окна командной строки.
ms.topic: reference
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f4aaaf198a898589699547c522a734e9e3e5aba2
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156725"
---
# <a name="title"></a>title

Создает заголовок для окна командной строки.

## <a name="syntax"></a>Синтаксис

```
title [<string>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<string>` | Задает текст, отображаемый в качестве заголовка окна командной строки. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Чтобы создать заголовок окна для пакетных программ, включите команду **Title** в начало пакетной программы.

- После установки заголовка окна его можно сбросить только с помощью команды **Title** .

## <a name="examples"></a>Примеры

Чтобы изменить заголовок окна командной строки для *обновления файлов* во время выполнения пакетным файлом команды **копирования** , а затем для возвращения заголовка в *командную строку*, введите следующий скрипт:

```
@echo off
title Updating Files
copy \\server\share\*.xls c:\users\common\*.xls
echo Files Updated.
title Command Prompt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
