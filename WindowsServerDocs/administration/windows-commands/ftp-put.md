---
title: ftp put
description: Справочная статья по команде FTP-размещения, которая копирует локальный файл на удаленный компьютер, используя текущий тип перемещения файлов.
ms.topic: reference
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/30/2020
ms.openlocfilehash: 24877dc154d7e88796eb3fc685351eee0c38c377
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624738"
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

| Параметр | Описание |
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
