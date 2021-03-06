---
title: extract
description: Справочная статья по команде Extract, которая извлекает файлы из исходного расположения.
ms.topic: reference
ms.assetid: 20dab03e-f6e1-4eb8-b8a1-fd6f1d97ee83
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 12/29/2020
ms.openlocfilehash: 47a31ae1d406aa08a6cab8271d8c94695b416758
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101818198"
---
# <a name="extract--extrac32"></a>Extract/extrac32

Извлекает файлы из CAB-файла или из источника.

> [!NOTE]
> В Windows Server 2016 и более поздних версиях и в Windows 10 Extract.exe файл программы не предоставляется и не поддерживается.
> Он заменяется Extrac32.exe, который изначально входит в состав Internet Explorer и теперь входит в состав операционной системы.

## <a name="syntax"></a>Синтаксис

## <a name="extractexe"></a>Extract.exe

```
extract [/y] [/a] [/d | /e] [/l dir] cabinet [filename ...]
extract [/y] source [newname]
extract [/y] /c source destination
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| файле | Используйте, если требуется извлечь два или более файлов. |
| имя_файла | Имя файла, извлекаемого из CAB-архива. Можно использовать подстановочные знаки и несколько имен файлов (разделенные пробелами). |
| source | Сжатый файл (CAB-файл с одним файлом). |
| newname | Новое имя файла, чтобы получить извлеченный файл. Если значение не указано, используется исходное имя. |
| /a | Обработка всех ящиков. Ниже приведена цепочка CAB-файлов, начиная с первого указанного CAB-файла. |
| /C | Копировать исходный файл в место назначения (для копирования с дисков DMF). |
| /d | Откройте каталог CAB-файлов (используйте с именем filename, чтобы избежать извлечения). |
| /e | Extract (используйте вместо *.* для извлечения всех файлов). |
| /l dir | Расположение для размещения извлеченных файлов (по умолчанию текущий каталог). |
| /y | Не выдавать запрос перед перезаписыванием существующего файла. |

## <a name="extrac32exe"></a>Extrac32.exe

> [!NOTE]
> Extrac32.exe можно использовать из командной строки, но не отображает выходные данные в консоли.
> Перенаправление вывода справки с помощью команды [More](https://docs.microsoft.com/windows-server/administration/windows-commands/more) , например: `extrac32.exe /? | more`

```
Extrac32 [/Y] [/A] [/D | /E] [/L dir] cabinet [filename ...]
Extrac32 [/Y] source [newname]
Extrac32 [/Y] /C source destination
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| :-------- | :---------- |
| файле   | CAB-файл (содержит два или более файлов). |
| имя_файла  | Имя файла, извлекаемого из CAB-архива. Можно использовать подстановочные знаки и несколько имен файлов (разделенные пробелами). |
| source    | Сжатый файл (CAB-файл с одним файлом). |
| newname   | Новое имя файла, чтобы получить извлеченный файл. Если значение не указано, используется исходное имя. |
| /A        | Обработка всех ящиков.  Ниже приведена цепочка CAB-файлов, начиная с первого указанного CAB-файла. |
| /C        | Копировать исходный файл в место назначения (для копирования с дисков DMF). |
| /D        | Откройте каталог CAB-файлов (используйте с именем filename, чтобы избежать извлечения). |
| /E        | Extract (используйте вместо *.* для извлечения всех файлов). |
| /L dir    | Расположение для размещения извлеченных файлов (по умолчанию текущий каталог). |
| /Y        | Не выдавать запрос перед перезаписыванием существующего файла. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
