---
title: title
description: Справочная статья по команде Title, которая создает заголовок для окна командной строки.
ms.topic: reference
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 81d5fdbf875733696dff93e6abec968db34a40cb
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805027"
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
