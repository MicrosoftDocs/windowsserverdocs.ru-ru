---
title: ftp mdelete
description: Справочная статья по команде FTP мделете, которая удаляет файлы на удаленном компьютере.
ms.topic: reference
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 647f7aa532f15e5391f68ef2121766e9aa31ff85
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038895"
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
