---
title: ftp delete
description: Справочная статья по команде FTP DELETE, которая удаляет файлы на удаленных компьютерах.
ms.topic: reference
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7a09e9abbe23582a2b5f2ba197a1877ffc62c7cc
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624798"
---
# <a name="ftp-delete"></a>ftp delete

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет файлы на удаленных компьютерах.

## <a name="syntax"></a>Синтаксис

```
delete <remotefile>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<remotefile>` | Указывает файл для удаления. |

### <a name="examples"></a>Примеры

Чтобы удалить файл *test.txt* на удаленном компьютере, введите:

```
delete test.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
