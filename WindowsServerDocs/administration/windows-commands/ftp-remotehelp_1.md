---
title: ftp remotehelp
description: Справочная статья по команде FTP ремотехелп, которая отображает справку по удаленным командам.
ms.topic: reference
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c91fda83ea988f79237b27f6df6bd6062748e37c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639374"
---
# <a name="ftp-remotehelp"></a>ftp remotehelp

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает справку по удаленным командам.

## <a name="syntax"></a>Синтаксис

```
remotehelp [<command>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| ------- | -------- |
| `[<command>]` | Указывает имя команды, для которой требуется справка. Если `<command>` не указан, эта команда отображает список всех удаленных команд. Можно также выполнять удаленные команды с помощью [предложения FTP](ftp-quote.md) или [литерала FTP](ftp-literal_1.md). |

### <a name="examples"></a>Примеры

Чтобы отобразить список удаленных команд, введите:

```
remotehelp
```

Чтобы отобразить синтаксис удаленной команды *достижением* , введите:

```
remotehelp feat
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [ftp quote](ftp-quote.md)

- [ftp literal](ftp-literal_1.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
