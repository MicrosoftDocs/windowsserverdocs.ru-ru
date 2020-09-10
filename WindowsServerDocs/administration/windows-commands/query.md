---
title: query
description: Справочная статья по команде запроса, в которой отображаются сведения о процессах, сеансах и удаленный рабочий стол серверах узлов сеансов.
ms.topic: reference
ms.assetid: 675c5128-f3cf-4e8f-8a3f-b29ab2a8b6de
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 62719f6ace4f27e46701958180811118886929a8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637426"
---
# <a name="query"></a>query

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сведения о процессах, сеансах и удаленный рабочий стол серверах узлов сеансов. Чтобы узнать о новых возможностях последней версии, см. статью [новые возможности службы удаленных рабочих столов в Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Синтаксис

```
query process
query session
query termserver
query user
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| [query process](query-process.md) | Отображает сведения о процессах, запущенных на сервере узла сеансов удаленный рабочий стол. |
| [query session](query-session.md) | Отображает сведения о сеансах на сервере узла сеансов удаленный рабочий стол. |
| [query termserver](query-termserver.md) | Отображает список всех удаленный рабочий стол серверов узлов сеансов в сети. |
| [query user](query-user.md) | Отображает сведения о пользовательских сеансах на удаленный рабочий стол сервере узла сеансов. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Справочник по командам служб удаленных рабочих столов (служб терминалов)](remote-desktop-services-terminal-services-command-reference.md)
