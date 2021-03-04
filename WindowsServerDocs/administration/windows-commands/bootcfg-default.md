---
title: bootcfg default
description: Справочная статья по команде bootcfg по умолчанию, которая указывает запись операционной системы для обозначения по умолчанию.
ms.topic: reference
ms.assetid: e21824d7-8278-41d7-a2c5-ce09803d513a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f0cc9bb0df002cf3b674571bc289b04fd5969c89
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820388"
---
# <a name="bootcfg-default"></a>bootcfg default

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Указывает запись операционной системы, которую следует назначить по умолчанию.

## <a name="syntax"></a>Синтаксис

```
bootcfg /default [/s <computer> [/u <domain>\<user> /p <password>]] [/id <osentrylinenum>]
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

Для использования команды **bootcfg/default** :

```
bootcfg /default /id 2
bootcfg /default /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда bootcfg](bootcfg.md)
