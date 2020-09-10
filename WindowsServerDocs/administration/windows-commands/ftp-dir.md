---
title: ftp dir
description: Справочная статья по команде FTP dir, которая отображает список файлов каталога и подкаталогов на удаленном компьютере.
ms.topic: reference
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8641fdca55976eb5998cdfbba58eddd3e6d8f286
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89621785"
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

Чтобы сохранить список текущего каталога на удаленном компьютере в *dirlist.txt*локального файла, введите:

```
dir . dirlist.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
