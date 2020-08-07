---
title: ftp mget
description: Справочная статья по команде FTP mget, которая копирует удаленные файлы на локальный компьютер, используя текущий тип перемещения файлов.
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9074df66e70961c74ef1b479f31ac316e34ff051
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889333"
---
# <a name="ftp-mget"></a>ftp mget

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Копирует удаленные файлы на локальный компьютер, используя текущий тип перемещения файлов.

## <a name="syntax"></a>Синтаксис

```
mget <remotefile>[ ]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<remotefile>` | Указывает удаленные файлы, которые необходимо скопировать на локальный компьютер. |

### <a name="examples"></a>Примеры

Чтобы скопировать удаленные файлы *a.exe* и *b.exe* на локальный компьютер, используя текущий тип перемещения файлов, введите:

```
mget a.exe b.exe
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда FTP ASCII](ftp-ascii.md)

- [Двоичная команда FTP](ftp-binary.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
