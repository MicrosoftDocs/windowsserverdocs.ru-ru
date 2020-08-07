---
title: ftp mput
description: Справочная статья по команде FTP мпут, которая копирует локальные файлы на удаленный компьютер, используя текущий тип перемещения файлов.
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d2caf7e91341f470fc265d0d1dbf6a51b6fe99bb
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889231"
---
# <a name="ftp-mput"></a>ftp mput

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Копирует локальные файлы на удаленный компьютер, используя текущий тип перемещения файлов.

## <a name="syntax"></a>Синтаксис

```
mput <localfile>[ ]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<localfile>` | Указывает локальный файл для копирования на удаленный компьютер. |

### <a name="examples"></a>Примеры

Чтобы скопировать *Program1.exe* и *Program2.exe* на удаленный компьютер, используя текущий тип перемещения файлов, введите:

```
mput Program1.exe Program2.exe
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда FTP ASCII](ftp-ascii.md)

- [Двоичная команда FTP](ftp-binary.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
