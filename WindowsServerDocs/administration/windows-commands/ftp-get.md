---
title: ftp get
description: Справочная статья по команде FTP Get, которая копирует удаленный файл на локальный компьютер, используя текущий тип перемещения файлов.
ms.topic: reference
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: cd8b39b596398cb670f5ec5b37932cfdaef65895
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817808"
---
# <a name="ftp-get"></a>ftp get

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Копирует удаленный файл на локальный компьютер, используя текущий тип перемещения файлов.

> [!NOTE]
> Эта команда совпадает с [командой FTP recv](ftp-recv.md).

## <a name="syntax"></a>Синтаксис

```
get <remotefile> [<localfile>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<remotefile>` | Указывает удаленный файл для копирования. |
| `[<localfile>]` | Указывает имя файла, используемого на локальном компьютере. Если параметр *локальный_файл* не указан, файлу присваивается имя *ремотефиле*. |

### <a name="examples"></a>Примеры

Чтобы скопировать *test.txt* на локальный компьютер, используя текущий перенос файлов, введите:

```
get test.txt
```

Чтобы скопировать *test.txt* на локальный компьютер как *test1.txt* с использованием текущей пересылки файлов, введите:

```
get test.txt test1.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда FTP recv](ftp-recv.md)

- [Команда FTP ASCII](ftp-ascii.md)

- [Двоичная команда FTP](ftp-binary.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
