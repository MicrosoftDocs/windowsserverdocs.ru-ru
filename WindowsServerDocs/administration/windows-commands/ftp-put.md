---
title: ftp put
description: Справочная статья по команде FTP-размещения, которая копирует локальный файл на удаленный компьютер, используя текущий тип перемещения файлов.
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/30/2020
ms.openlocfilehash: e0794c12d7e613f92546903586fe14d23319185a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889123"
---
# <a name="ftp-put"></a>ftp put

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Копирует локальный файл на удаленный компьютер, используя текущий тип перемещения файлов.

> [!NOTE]
> Эта команда совпадает с [командой FTP Send](ftp-send_1.md).

## <a name="syntax"></a>Синтаксис

```
put <localfile> [<remotefile>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<localfile>` | Указывает локальный файл для копирования. |
| `[<remotefile>]` | Указывает имя, используемое на удаленном компьютере. Если не указать *ремотефиле*, файл будет давать имя *локальный_файл* .|

### <a name="examples"></a>Примеры

Чтобы скопировать локальный файл *test.txt* и присвоить ему имя *test1.txt* на удаленном компьютере, введите:

```
put test.txt test1.txt
```

Чтобы скопировать локальный файл *program.exe* на удаленный компьютер, введите:

```
put program.exe
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда FTP ASCII](ftp-ascii.md)

- [Двоичная команда FTP](ftp-binary.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
