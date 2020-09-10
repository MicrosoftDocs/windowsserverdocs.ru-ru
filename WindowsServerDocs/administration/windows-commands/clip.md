---
title: clip
description: Справочная статья для команды Clip, которая перенаправляет выходные данные команды из командной строки в буфер обмена Windows.
ms.topic: reference
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9f6820d60a8c94ed07bbb23bbbd86be3f1f289b7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89629624"
---
# <a name="clip"></a>clip

Перенаправляет выходные данные команды из командной строки в буфер обмена Windows. Эту команду можно использовать для копирования данных непосредственно в любое приложение, которое может получить текст из буфера обмена. Этот текстовый вывод также можно вставить в другие программы.

## <a name="syntax"></a>Синтаксис

```
<command> | clip
clip < <filename>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<command>` | Указывает команду, выходные данные которой нужно отправить в буфер обмена Windows. |
| `<filename>` | Указывает файл, содержимое которого необходимо отправить в буфер обмена Windows. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы скопировать текущий список каталогов в буфер обмена Windows, введите:

```
dir | clip
```

Чтобы скопировать выходные данные программы с именем *Generic. awk* в буфер обмена Windows, введите:

```
awk -f generic.awk input.txt | clip
```

Чтобы скопировать содержимое файла с именем *readme.txt* в буфер обмена Windows, введите:

```
clip < readme.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)