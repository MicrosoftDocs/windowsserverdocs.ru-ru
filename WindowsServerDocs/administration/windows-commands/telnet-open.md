---
title: telnet open
description: Справочная статья по команде Telnet Open, которая подключается к серверу Telnet.
s.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6db7f428f4b8c85c6e953a8fe4a9328b965898f8
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718011"
---
# <a name="telnet-open"></a>Telnet: открыть

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Подключается к серверу Telnet.

## <a name="syntax"></a>Синтаксис

```
o[pen] <hostname> [<port>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<hostname>` | Указывает имя или IP-адрес компьютера. |
| `[<port>]` | Указывает TCP-порт, который прослушивает сервер Telnet. Значение по умолчанию — TCP-порт 23. |

## <a name="examples"></a>Примеры

Чтобы подключиться к серверу Telnet по адресу *Telnet.Microsoft.com*, введите:

```
o telnet.microsoft.com
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
