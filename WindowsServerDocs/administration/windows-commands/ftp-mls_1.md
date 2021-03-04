---
title: ftp mls
description: Справочная статья по команде FTP MLS, которая отображает сокращенный список файлов и подкаталогов в удаленном каталоге.
ms.topic: reference
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f8a7fcf0a14950999795189d21c9d4d46b0a4388
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817586"
---
# <a name="ftp-mls"></a>ftp mls

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сокращенный список файлов и подкаталогов в удаленном каталоге.

## <a name="syntax"></a>Синтаксис

```
mls <remotefile>[ ] <localfile>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<remotefile>` | Указывает файл, для которого требуется просмотреть список. При указании *ремотефилес* Используйте дефис для представления текущего рабочего каталога на удаленном компьютере. |
| `<localfile>` | Указывает локальный файл для хранения списка. При указании параметра *локальный_файл* Используйте дефис для отображения списка на экране. |

### <a name="examples"></a>Примеры

Чтобы отобразить сокращенный список файлов и подкаталогов для *Dir1* и *Dir2*, введите:

```
mls dir1 dir2 -
```

Чтобы сохранить сокращенный список файлов и подкаталогов для *Dir1* и *Dir2* в локальном файле *dirlist.txt*, введите:

```
mls dir1 dir2 dirlist.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
