---
title: ren
description: Справочная статья по команде REN, которая переименовывает файл или каталог.
ms.topic: reference
ms.assetid: 60398e12-a05d-4524-a73a-0a925943e21d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 96ffae30ff5652f0493f31c9aa839bd213f2be25
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806987"
---
# <a name="ren"></a>ren

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Переименовывает файлы или каталоги.

> [!NOTE]
> Эта команда аналогична [команде Rename](rename.md).

## <a name="syntax"></a>Синтаксис

```
ren [<drive>:][<path>]<filename1> <filename2>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `[<drive>:][<path>]<filename1>` | Указывает расположение и имя файла или набора файлов, которые требуется переименовать. *Имя_файла1* может содержать подстановочные знаки (**&#42;** и **?**). |
| `<filename2>` | Указывает новое имя для файла. Для указания новых имен нескольких файлов можно использовать подстановочные знаки. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- При переименовании файлов нельзя указывать новый диск или путь. Эту команду также нельзя использовать для переименования файлов на дисках или для перемещения файлов в другой каталог.

- Символы, представленные подстановочными знаками в *имя_файла2* , будут совпадать с соответствующими символами в *имя_файла1*.

- *Имя_файла2* должно быть уникальным именем файла. Если параметр *имя_файла2* совпадает с существующим именем файла, появляется следующее сообщение: `Duplicate file name or file not found` .

### <a name="examples"></a>Примеры

Чтобы изменить все расширения имени файла txt в текущем каталоге на расширения DOC, введите:

```
ren *.txt *.doc
```

Чтобы изменить имя каталога с *Chap10* на *Part10*, введите:

```
ren chap10 part10
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда "Переименовать"](rename.md)
