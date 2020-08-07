---
title: ftp send
description: Справочная статья по команде FTP Send, которая копирует локальный файл на удаленный компьютер с использованием текущего типа передачи файлов.
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 93b2af82954535d409eb16ab46c0feb918e18b21
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888931"
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

| Параметр | Описание: |
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
