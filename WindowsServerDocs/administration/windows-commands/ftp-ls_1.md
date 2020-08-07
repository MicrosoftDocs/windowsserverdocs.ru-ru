---
title: ftp ls
description: Справочная статья по команде FTP Ls, которая отображает сокращенный список файлов и подкаталогов с удаленного компьютера.
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 59e19d7e48b902ccc0704c22e150b3494fb2ad2b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889347"
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
