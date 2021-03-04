---
title: bootcfg query
description: Справочная статья по команде bootcfg query, которая запрашивает и отображает записи раздела Boot Loader и операционной системы из Boot.ini.
ms.topic: reference
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b572eca783082cb2f72e380cdb98a0d1932e1041
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820278"
---
# <a name="bootcfg-query"></a>bootcfg query

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Запрашивает и отображает записи разделов [boot loader] и [Operating Systems] из Boot.ini.

## <a name="syntax"></a>Синтаксис

```
bootcfg /query [/s <computer> [/u <domain>\<user> /p <password>]]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `/s <computer>` | Указывает имя или IP-адрес удаленного компьютера (не используйте обратную косую черту). По умолчанию это локальный компьютер. |
| `/u <domain>\<user>`  | Выполняет команду с разрешениями учетной записи пользователя, указанного в параметре `<user>` или `<domain>\<user>` . По умолчанию заданы разрешения текущего вошедшего в систему пользователя на компьютере, выполняющем команду. |
| `/p <password>` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . |
| /? | Отображение справки в командной строке. |

#### <a name="sample-output"></a>Пример выходных данных

Пример выходных данных для команды **bootcfg/query** :

```
Boot Loader Settings
----------
timeout: 30
default: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
Boot Entries
------
Boot entry ID:   1
Friendly Name:
path: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
OS Load Options: /fastdetect /debug /debugport=com1:
```

- В области **параметры загрузчика** отображаются все записи в разделе [boot loader] Boot.ini.

- В области **загрузочные записи** отображаются дополнительные сведения для каждой записи операционной системы в разделе [operating systems] Boot.ini

## <a name="examples"></a>Примеры

Для использования команды **bootcfg/query** :

```
bootcfg /query
bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
bootcfg /query /u hiropln /p p@ssW23
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда bootcfg](bootcfg.md)
