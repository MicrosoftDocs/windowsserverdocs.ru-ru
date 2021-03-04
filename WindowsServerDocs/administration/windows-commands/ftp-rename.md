---
title: ftp rename
description: Справочная статья по команде FTP Rename, которая переименовывает удаленные файлы.
ms.topic: reference
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 89eafff6ed8577c907fc680ba0461387daf53296
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817408"
---
# <a name="ftp-rename"></a>ftp rename

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Переименовывает удаленные файлы.

## <a name="syntax"></a>Синтаксис

```
rename <filename> <newfilename>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<filename>` | Указывает файл, который требуется переименовать. |
| `<newfilename>` | Указывает новое имя файла. |

### <a name="examples"></a>Примеры

Чтобы переименовать удаленный файл *example.txt* в *example1.txt*, введите:

```
rename example.txt example1.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
