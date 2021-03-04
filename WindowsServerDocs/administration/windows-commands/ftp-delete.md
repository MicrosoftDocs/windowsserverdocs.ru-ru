---
title: ftp delete
description: Справочная статья по команде FTP DELETE, которая удаляет файлы на удаленных компьютерах.
ms.topic: reference
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e69891acc5dee6df874a883ef51ec471040e75cd
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817828"
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
