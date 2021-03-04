---
title: ftp ls
description: Справочная статья по команде FTP Ls, которая отображает сокращенный список файлов и подкаталогов с удаленного компьютера.
ms.topic: reference
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 78a69000797703e414351e3c3d566909cb5bb269
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817648"
---
# <a name="ftp-ls"></a>ftp ls

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сокращенный список файлов и подкаталогов с удаленного компьютера.

## <a name="syntax"></a>Синтаксис

```
ls [<remotedirectory>] [<localfile>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- |------------ |
| `[<remotedirectory>]` | Указывает каталог, для которого требуется просмотреть список. Если каталог не указан, используется текущий рабочий каталог на удаленном компьютере. |
| `[<localfile>]` | Указывает локальный файл для хранения списка. Если локальный файл не указан, результаты отображаются на экране. |

### <a name="examples"></a>Примеры

Чтобы отобразить сокращенный список файлов и подкаталогов на удаленном компьютере, введите:

```
ls
```

Чтобы получить сокращенный список каталогов *Dir1* на удаленном компьютере и сохранить его в локальном файле с именем *dirlist.txt*, введите:

```
ls dir1 dirlist.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
