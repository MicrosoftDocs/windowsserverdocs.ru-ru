---
title: ftp mdelete
description: Справочная статья по команде FTP мделете, которая удаляет файлы на удаленном компьютере.
ms.topic: reference
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 65e7d924a624af079ec7254179c847297669bc8d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817211"
---
# <a name="ftp-mdelete"></a>ftp mdelete

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет файлы на удаленном компьютере.

## <a name="syntax"></a>Синтаксис
```
mdelete <remotefile>[...]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<remotefile>` | Указывает удаленный файл для удаления. |

### <a name="examples"></a>Примеры

Чтобы удалить удаленные файлы *a.exe* и *b.exe*, введите:

```
mdelete a.exe b.exe
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
