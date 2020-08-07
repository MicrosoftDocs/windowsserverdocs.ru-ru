---
title: bootcfg delete
description: Справочная статья по команде bootcfg DELETE, которая удаляет запись операционной системы в разделе "операционные системы" файла Boot.ini.
ms.topic: article
ms.assetid: 71382e29-9b39-41c8-9c23-cf0ff829440a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2426dde90402e65eb29c78d82562338a61248cf6
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880618"
---
# <a name="bootcfg-delete"></a>bootcfg delete

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет запись операционной системы в разделе [Operating Systems] файла Boot.ini.

## <a name="syntax"></a>Синтаксис

```
bootcfg /delete [/s <computer> [/u <domain>\<user> /p <password>]] [/id <osentrylinenum>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `/s <computer>` | Указывает имя или IP-адрес удаленного компьютера (не используйте обратную косую черту). По умолчанию это локальный компьютер. |
| `/u <domain>\<user>`  | Выполняет команду с разрешениями учетной записи пользователя, указанного в параметре `<user>` или `<domain>\<user>` . По умолчанию заданы разрешения текущего вошедшего в систему пользователя на компьютере, выполняющем команду. |
| `/p <password>` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . |
| `/id <osentrylinenum>` | Указывает номер строки записи операционной системы в разделе [Operating Systems] файла Boot.ini, в который добавляются параметры загрузки операционной системы. Первая строка после заголовка раздела [Operating Systems] — 1. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы использовать команду **bootcfg/Delete** , выполните следующие действия.

```
bootcfg /delete /id 1
bootcfg /delete /s srvmain /u maindom\hiropln /p p@ssW23 /id 3
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда bootcfg](bootcfg.md)
