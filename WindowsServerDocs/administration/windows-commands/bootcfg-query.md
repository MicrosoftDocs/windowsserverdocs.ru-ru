---
title: bootcfg query
description: Справочная статья по команде bootcfg query, которая запрашивает и отображает записи раздела Boot Loader и операционной системы из Boot.ini.
ms.topic: reference
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8debee9f799a89f80c82b25242127c42fd00189f
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630198"
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
