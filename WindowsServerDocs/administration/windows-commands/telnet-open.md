---
title: telnet open
description: Справочная статья по команде Telnet Open, которая подключается к серверу Telnet.
ms.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3ce606395530fee08de7ceaf6fe2a0f7243b5b97
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946890"
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
