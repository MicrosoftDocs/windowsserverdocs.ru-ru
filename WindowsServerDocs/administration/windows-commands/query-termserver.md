---
title: query termserver
description: Справочная статья по команде Query термсервер, в которой отображается список всех удаленный рабочий стол серверов узлов сеансов в сети.
ms.topic: reference
ms.assetid: 3b89d3b4-236f-4376-90b6-939a0ec4b288
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 33abf76e66b2d42cf0368503fa3a6e119dc1fd1c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639874"
---
# <a name="query-termserver"></a>query termserver

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает список всех удаленный рабочий стол серверов узлов сеансов в сети. Эта команда ищет в сети все подключенные удаленный рабочий стол серверы узлов сеансов и возвращает следующие сведения:

- Имя сервера

- Сеть (и адрес узла, если используется параметр/Аддресс)

> [!NOTE]
> Чтобы узнать о новых возможностях последней версии, см. статью [новые возможности службы удаленных рабочих столов в Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Синтаксис

```
query termserver [<servername>] [/domain:<domain>] [/address] [/continue]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<servername>` | Указывает имя, идентифицирующее сервер узла сеансов удаленный рабочий стол. |
| /Domain`<domain>` | Указывает домен для запроса серверов терминалов. Не нужно указывать домен, если выполняется запрос к домену, в котором вы работаете в данный момент. |
| /аддресс | Отображает адреса сети и узла для каждого сервера. |
| /континуе | Предотвращает приостановку после отображения каждого экрана информации. |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

Чтобы отобразить сведения обо всех серверах узлов сеансов удаленный рабочий стол в сети, введите:

```
query termserver
```

Чтобы отобразить сведения о удаленный рабочий стол сервере узла сеансов с именем *Server3*, введите:

```
query termserver Server3
```

Чтобы отобразить сведения обо всех удаленный рабочий стол серверах узлов сеансов в домене *contoso*, введите:

```
query termserver /domain:CONTOSO
```

Чтобы отобразить адрес сети и узла для удаленный рабочий стол сервера узла сеансов с именем *Server3*, введите:

```
query termserver Server3 /address
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда запроса](query.md)

- [Справочник по командам служб удаленных рабочих столов (служб терминалов)](remote-desktop-services-terminal-services-command-reference.md)
