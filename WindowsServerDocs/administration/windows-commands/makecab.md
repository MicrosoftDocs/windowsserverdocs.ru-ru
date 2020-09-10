---
title: makecab
description: Справочная статья по команде makecab, которая упаковывает существующие файлы в CAB-файл.
ms.topic: reference
ms.assetid: 4da95297-c593-427b-9f76-2f389c46cbf4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3ba4adf0d1cc94fc3fc1c5d4db15f641a5c30b90
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640180"
---
# <a name="makecab"></a>makecab

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Упакуйте существующие файлы в CAB-файл.


> [!NOTE]
> Эта команда аналогична [команде диантз](diantz.md).

## <a name="syntax"></a>Синтаксис

```
makecab [/v[n]] [/d var=<value> ...] [/l <dir>] <source> [<destination>]
makecab [/v[<n>]] [/d var=<value> ...] /f <directives_file> [...]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<source>` | Файл для сжатия. |
| `<destination>` | Имя файла для предоставления сжатого файла. Если этот параметр опущен, последний символ имени исходного файла заменяется символом подчеркивания (_) и используется в качестве назначения. |
| /f `<directives_file>` | Файл с директивами **makecab** (может повторяться). |
| /d var =`<value>` | Определяет переменную с указанным значением. |
| /l `<dir>` | Расположение для размещения назначения (по умолчанию текущий каталог). |
| /v [ `<n>` ] | Задать уровень детализации отладки (0 = нет,..., 3 = полный). |
| /? | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда диантз](diantz.md)

- [Формат CAB-файла Microsoft](/previous-versions/bb417343(v=msdn.10))
