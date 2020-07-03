---
title: eventcreate
description: Справочная статья по команде eventcreate, которая позволяет администратору создать пользовательское событие в указанном журнале событий.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2b1b26d-a70e-49a6-832b-91eb5a1a159a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60ed97eeffc8ae2410fdd8f296a0e8348f376652
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925319"
---
# <a name="eventcreate"></a>eventcreate

Позволяет администратору создать пользовательское событие в указанном журнале событий.

> [!IMPORTANT]
> Пользовательские события не могут быть записаны в журнал безопасности.

## <a name="syntax"></a>Синтаксис

```
eventcreate [/s <computer> [/u <domain\user> [/p <password>]] {[/l {APPLICATION|SYSTEM}]|[/so <srcname>]} /t {ERROR|WARNING|INFORMATION|SUCCESSAUDIT|FAILUREAUDIT} /id <eventID> /d <description>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- |------------ |
| ключ`<computer>` | Указывает имя или IP-адрес удаленного компьютера (не используйте символы обратной косой черты). По умолчанию это локальный компьютер. |
| /u`<domain\user>` | Выполняет команду с разрешениями учетной записи пользователя, указанного в параметре `<user>` или `<domain\user>` . По умолчанию заданы разрешения текущего вошедшего в систему пользователя на компьютере, выполняющем команду. |
| /p`<password>` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . |
| /l`{APPLICATION | SYSTEM}` | Указывает имя журнала событий, в котором будет создано событие. Допустимые имена журналов — **Application** или **System**. |
| /So`<srcname>` | Указывает источник, используемый для события. Допустимым источником может быть любая строка, которая должна представлять приложение или компонент, создающий событие. |
| /t`{ERROR | WARNING | INFORMATION | SUCCESSAUDIT | FAILUREAUDIT}` | Указывает тип создаваемого события. Допустимые типы: **Error**, **warning**, **Information**, **SUCCESSAUDIT**и **FAILUREAUDIT**. |
| /ID`<eventID>` | Указывает идентификатор события для события. Допустимый идентификатор — любое число от 1 до 1000. |
| /d`<description>` | Указывает описание, используемое для вновь созданного события. |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

В следующих примерах показано, как можно использовать команду **eventcreate** :

```
eventcreate /t error /id 100 /l application /d Create event in application log
eventcreate /t information /id 1000 /so winmgmt /d Create event in WinMgmt source
eventcreate /t error /id 2001 /so winword /l application /d new src Winword in application log
eventcreate /s server /t error /id 100 /l application /d Remote machine without user credentials
eventcreate /s server /u user /p password /id 100 /t error /l application /d Remote machine with user credentials
eventcreate /s server1 /s server2 /u user /p password /id 100 /t error /so winmgmt /d Creating events on Multiple remote machines
eventcreate /s server /u user /id 100 /t warning /so winmgmt /d Remote machine with partial user credentials
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
