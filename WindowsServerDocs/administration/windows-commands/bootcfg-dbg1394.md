---
title: bootcfg dbg1394
description: Справочная статья по команде bootcfg dbg1394, которая настраивает отладку порта 1394 для указанной записи операционной системы.
ms.topic: reference
ms.assetid: 35724697-90dd-4dbe-85b0-337fbd369dcc
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 85cd442dc4d29291f33194c76c2f336b4d180d9e
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820408"
---
# <a name="bootcfg-dbg1394"></a>bootcfg dbg1394

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Настраивает отладку порта 1394 для указанной записи операционной системы.

## <a name="syntax"></a>Синтаксис

```
bootcfg /dbg1394 {on | off}[/s <computer> [/u <domain>\<user> /p <password>]] [/ch <channel>] /id <osentrylinenum>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `{on | off}` | Указывает значение для отладки порта 1394, включая:<ul><li>**on.** Включает поддержку удаленной отладки путем добавления параметра/dbg1394 к указанному `<osentrylinenum>` .</li><li>**автоном.** Отключает поддержку удаленной отладки путем удаления параметра/dbg1394 из указанного <osentrylinenum> .</li></ul> |
| `/s <computer>` | Указывает имя или IP-адрес удаленного компьютера (не используйте обратную косую черту). По умолчанию это локальный компьютер. |
| `/u <domain>\<user>`  | Выполняет команду с разрешениями учетной записи пользователя, указанного в параметре `<user>` или `<domain>\<user>` . По умолчанию заданы разрешения текущего вошедшего в систему пользователя на компьютере, выполняющем команду. |
| `/p <password>` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . |
| `/ch <channel>` | Указывает канал, используемый для отладки. Допустимые значения включают целые числа от 1 до 64. Не используйте этот параметр, если отладка порта 1394 отключена. |
| `/id <osentrylinenum>` | Указывает номер строки записи операционной системы в разделе [Operating Systems] файла Boot.ini, в который добавляются параметры загрузки операционной системы. Первая строка после заголовка раздела [Operating Systems] — 1. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы использовать команду **bootcfg/dbg1394**, выполните следующие действия.

```
bootcfg /dbg1394 /id 2
bootcfg /dbg1394 on /ch 1 /id 3
bootcfg /dbg1394 edit /ch 8 /id 2
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /dbg1394 off /id 2
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда bootcfg](bootcfg.md)
