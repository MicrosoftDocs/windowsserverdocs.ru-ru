---
title: ftp recv
description: Справочная статья по команде FTP recv, которая копирует удаленный файл на локальный компьютер, используя текущий тип перемещения файлов.
ms.topic: article
ms.assetid: f249ce61-247d-421b-9b93-48bce5108800
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 888acc77ec4f6edc57d9d1bed76563538f621eb5
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889059"
---
# <a name="ftp-recv"></a>ftp recv

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Копирует удаленный файл на локальный компьютер, используя текущий тип перемещения файлов.

> [!NOTE]
> Эта команда совпадает с [командой FTP Get](ftp-get.md).

## <a name="syntax"></a>Синтаксис

```
recv <remotefile> [<localfile>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<remotefile>` | Указывает удаленный файл для копирования. |
| `[<localfile>]` | Указывает имя файла, используемого на локальном компьютере. Если параметр *локальный_файл* не указан, файлу присваивается имя *ремотефиле*. |

### <a name="examples"></a>Примеры

Чтобы скопировать *test.txt* на локальный компьютер, используя текущий перенос файлов, введите:

```
recv test.txt
```

Чтобы скопировать *test.txt* на локальный компьютер как *test1.txt* с использованием текущей пересылки файлов, введите:

```
recv test.txt test1.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Get FTP](ftp-get.md)

- [Команда FTP ASCII](ftp-ascii.md)

- [Двоичная команда FTP](ftp-binary.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
