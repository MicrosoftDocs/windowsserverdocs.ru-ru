---
title: ftp append
description: Справочная статья по команде FTP Append, которая добавляет локальный файл в файл на удаленном компьютере с использованием текущего параметра типа файла.
ms.topic: reference
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 42270b8f3633158e12d472a234fcf1904cee86de
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89638573"
---
# <a name="ftp-append"></a>ftp append

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет локальный файл в файл на удаленном компьютере, используя текущий параметр типа файла.

## <a name="syntax"></a>Синтаксис

```
append <localfile> [remotefile]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<localfile>` | Указывает локальный файл для добавления. |
| [ремотефиле] | Указывает файл на удаленном компьютере, к которому <localfile> добавляется. Если этот параметр не используется, вместо `<localfile>` имени удаленного файла используется имя. |

### <a name="examples"></a>Примеры

Чтобы добавить *file1.txt* *file2.txt* на удаленном компьютере, введите:

```
append file1.txt file2.txt
```

Чтобы добавить локальный *file1.txt* в файл с именем *file1.txt* на удаленном компьютере.

```
append file1.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
