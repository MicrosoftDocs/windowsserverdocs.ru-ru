---
title: ftp dir
description: Справочная статья по команде FTP dir, которая отображает список файлов каталога и подкаталогов на удаленном компьютере.
ms.topic: reference
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: aee07906ff43e235f0513b4139426e83ca9d4054
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817788"
---
# <a name="ftp-dir"></a>ftp dir

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает список файлов каталога и подкаталогов на удаленном компьютере.

## <a name="syntax"></a>Синтаксис

```
dir [<remotedirectory>] [<localfile>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| ------- | -------- |
| `[<remotedirectory>]` | Указывает каталог, для которого требуется просмотреть список. Если каталог не указан, используется текущий рабочий каталог на удаленном компьютере. |
| `[<localfile>]` | Указывает локальный файл, в котором будет храниться список каталогов. Если локальный файл не указан, результаты отображаются на экране. |

### <a name="examples"></a>Примеры

Чтобы отобразить список каталогов для *Dir1* на удаленном компьютере, введите:

```
dir dir1
```

Чтобы сохранить список текущего каталога на удаленном компьютере в *dirlist.txt* локального файла, введите:

```
dir . dirlist.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
