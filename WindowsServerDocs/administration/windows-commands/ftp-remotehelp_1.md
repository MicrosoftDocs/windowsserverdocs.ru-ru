---
title: ftp remotehelp
description: Справочная статья по команде FTP ремотехелп, которая отображает справку по удаленным командам.
ms.topic: reference
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e404b9c75d28c45feebb300d8538d9998b2d9753
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035792"
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
