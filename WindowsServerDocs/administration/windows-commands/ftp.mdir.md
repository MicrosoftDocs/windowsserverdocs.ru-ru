---
title: ftp mdir
description: Справочная статья по команде FTP мдир, которая отображает список каталогов файлов и подкаталогов в удаленном каталоге.
ms.topic: reference
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 48d29d6b1d26ccf09643b6845b2addde3ee5795f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817106"
---
# <a name="ftp-mdir"></a>ftp mdir

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает список каталогов файлов и подкаталогов в удаленном каталоге.

## <a name="syntax"></a>Синтаксис

```
mdir <remotefile>[...] <localfile>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<remotefile>` | Указывает каталог или файл, для которого требуется просмотреть список. Можно указать несколько *ремотефилес*. Введите дефис (-), чтобы использовать текущий рабочий каталог на удаленном компьютере. |
| `<localfile>` | Указывает локальный файл для хранения списка. Этот параметр обязателен. Введите дефис (-) для отображения списка на экране. |

### <a name="examples"></a>Примеры

Чтобы вывести на экран список каталогов *Dir1* и *Dir2* , введите:

```
mdir dir1 dir2 -
```

Чтобы сохранить Объединенный каталог со списком *Dir1* и *Dir2* в локальном файле с именем *dirlist.txt*, введите:

```
mdir dir1 dir2 dirlist.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
