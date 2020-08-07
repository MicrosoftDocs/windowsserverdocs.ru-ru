---
title: rem
description: Справочная статья по команде REM, которая записывает комментарии в скрипт, пакет или файл config.sys.
ms.topic: article
ms.assetid: 1a45b585-a83c-4ff6-badd-ff40f34cec23
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6593e7700853af3658206b741817a86933fa66d1
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883857"
---
# <a name="rem"></a>rem

Записывает комментарии в скрипт, пакет или файл config.sys. Если комментарий не указан, **REM** добавляется пробел по вертикали.

## <a name="syntax"></a>Синтаксис

```
rem [<comment>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
|--|--|
| `<comment>` | Указывает строку символов, включаемую в качестве комментария. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Remarks

- Команда **REM** не отображает комментарии на экране. Чтобы отобразить комментарии на экране, необходимо включить команду **echo on** в файл.

- `<`В комментариях пакетного файла нельзя использовать символ перенаправления (или `>` ) или pipe ( `|` ).

- Несмотря на то, что можно использовать **REM** без комментариев для добавления вертикальных пробелов в пакетный файл, можно также использовать пустые строки. При обработке пакетной программы пустые строки игнорируются.

### <a name="examples"></a>Примеры

Чтобы добавить вертикальные пробелы через комментарии пакетного файла, введите:

```
@echo off
rem  This batch program formats and checks new disks.
rem  It is named Checknew.bat.
rem
rem echo Insert new disk in Drive B.
pause
format b: /v chkdsk b:
```

Чтобы включить пояснительный комментарий перед командой **Prompt** в файле config.sys, введите:

```
rem Set prompt to indicate current directory
prompt $p$g
```

Чтобы предоставить комментарий о том, что делает сценарий, введите:

```
rem The commands in this script set up 3 drives.
rem The first drive is a primary partition and is
rem assigned the letter D. The second and third drives
rem are logical partitions, and are assigned letters
rem E and F.
create partition primary size=2048
assign d:
create partition extended
create partition logical size=2048
assign e:
create partition logical
assign f:
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)