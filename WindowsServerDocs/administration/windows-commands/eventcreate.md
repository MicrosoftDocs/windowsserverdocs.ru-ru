---
title: eventcreate
description: Справочная статья по команде eventcreate, которая позволяет администратору создать пользовательское событие в указанном журнале событий.
ms.topic: reference
ms.assetid: f2b1b26d-a70e-49a6-832b-91eb5a1a159a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d2fa1e4a90d0c24138c5353c5cf1b22308204d6f
ms.sourcegitcommit: 0b3d6661c44aa1a697087e644437279142726d84
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083655"
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
| ключ `<computer>` | Указывает имя или IP-адрес удаленного компьютера (не используйте символы обратной косой черты). По умолчанию это локальный компьютер. |
| /u `<domain\user>` | Выполняет команду с разрешениями учетной записи пользователя, указанного в параметре `<user>` или `<domain\user>` . По умолчанию заданы разрешения текущего вошедшего в систему пользователя на компьютере, выполняющем команду. |
| /p `<password>` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . |
| /l `{APPLICATION | SYSTEM}` | Указывает имя журнала событий, в котором будет создано событие. Допустимые имена журналов — **Application** или **System**. |
| /So `<srcname>` | Указывает источник, используемый для события. Допустимым источником может быть любая строка, которая должна представлять приложение или компонент, создающий событие. |
| /t `{ERROR | WARNING | INFORMATION | SUCCESSAUDIT | FAILUREAUDIT}` | Указывает тип создаваемого события. Допустимые типы: **Error**, **warning**, **Information**, **SUCCESSAUDIT**и **FAILUREAUDIT**. |
| /ID `<eventID>` | Указывает идентификатор события для события. Допустимый идентификатор — любое число от 1 до 1000. |
| /d `<description>` | Указывает описание, используемое для вновь созданного события. |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

В следующих примерах показано, как можно использовать команду **eventcreate** :

```
eventcreate /t ERROR /id 100 /l application /d "Create event in application log"
eventcreate /t INFORMATION /id 1000 /d "Create event in WinMgmt source"
eventcreate /t ERROR /id 201 /so winword /l application /d "New src Winword in application log"
eventcreate /s server /t ERROR /id 100 /l application /d "Remote machine without user credentials"
eventcreate /s server /u user /p password /id 100 /t ERROR /l application /d "Remote machine with user credentials"
eventcreate /s server1 /s server2 /u user /p password /id 100 /t ERROR /d "Creating events on Multiple remote machines"
eventcreate /s server /u user /id 100 /t WARNING /d "Remote machine with partial user credentials"
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
