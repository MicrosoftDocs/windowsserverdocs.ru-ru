---
title: ftp send
description: Справочная статья по команде FTP Send, которая копирует локальный файл на удаленный компьютер с использованием текущего типа передачи файлов.
ms.topic: reference
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0eba9b57f0401606afcbe84448683395140ceb3a
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817398"
---
# <a name="ftp-send"></a>ftp send

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Копирует локальный файл на удаленный компьютер, используя текущий тип перемещения файлов.

> [!NOTE]
> Эта команда совпадает с [командой FTP-размещения](ftp-put.md).

## <a name="syntax"></a>Синтаксис

```
send <localfile> [<remotefile>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<localfile>` | Указывает локальный файл для копирования. |
| `<remotefile>` | Указывает имя, используемое на удаленном компьютере. Если не указать *ремотефиле*, файл получит имя *локальный_файл* . |

### <a name="examples"></a>Примеры

Чтобы скопировать локальный файл *test.txt* и присвоить ему имя *test1.txt* на удаленном компьютере, введите:

```
send test.txt test1.txt
```

Чтобы скопировать локальный файл *program.exe* на удаленный компьютер, введите:

```
send program.exe
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
