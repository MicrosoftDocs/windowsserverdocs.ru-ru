---
title: ftp rename
description: Справочная статья по команде FTP Rename, которая переименовывает удаленные файлы.
ms.topic: reference
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ea7862a759779a5f767b8e18cdd5a0b36db2a6a1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627631"
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
