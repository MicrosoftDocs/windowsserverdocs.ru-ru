---
title: clip
description: Справочная статья для команды Clip, которая перенаправляет выходные данные команды из командной строки в буфер обмена Windows.
ms.topic: reference
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 84a5ac1e726f2842e9258357bf636b4f4a95e6df
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101819808"
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