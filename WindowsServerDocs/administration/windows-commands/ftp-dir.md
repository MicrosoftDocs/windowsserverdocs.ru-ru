---
title: ftp dir
description: Справочная статья по команде FTP dir, которая отображает список файлов каталога и подкаталогов на удаленном компьютере.
ms.topic: article
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a4f65cee67ec91b6871649fece4f580684c2e3f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889474"
---
# <a name="ftp-dir"></a>ftp dir

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает список файлов каталога и подкаталогов на удаленном компьютере.

## <a name="syntax"></a>Синтаксис

```
dir [<remotedirectory>] [<localfile>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| ------- | -------- |
| `[<remotedirectory>]` | Указывает каталог, для которого требуется просмотреть список. Если каталог не указан, используется текущий рабочий каталог на удаленном компьютере. |
| `[<localfile>]` | Указывает локальный файл, в котором будет храниться список каталогов. Если локальный файл не указан, результаты отображаются на экране. |

### <a name="examples"></a>Примеры

Чтобы отобразить список каталогов для *Dir1* на удаленном компьютере, введите:

```
dir dir1
```

Чтобы сохранить список текущего каталога на удаленном компьютере в *dirlist.txt*локального файла, введите:

```
dir . dirlist.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
