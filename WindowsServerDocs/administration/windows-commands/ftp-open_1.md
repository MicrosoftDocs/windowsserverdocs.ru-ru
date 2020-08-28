---
title: ftp open
description: Справочная статья по команде FTP Open, которая подключается к указанному FTP-серверу.
ms.topic: reference
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a7599eb4728a46655b4c3274a9d7708061c3a9ee
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89032822"
---
# <a name="ftp-open"></a>ftp open

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Подключается к указанному FTP-серверу.

## <a name="syntax"></a>Синтаксис

```
open <computer> [<port>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<computer>` | Указывает удаленный компьютер, к которому вы пытаетесь подключиться. Можно использовать IP-адрес или имя компьютера (в этом случае должен быть доступен DNS-сервер или файл Hosts). |
| `[<port>]` | Указывает номер порта TCP, используемый для подключения к FTP-серверу. По умолчанию используется TCP-порт 21. |

### <a name="examples"></a>Примеры

Чтобы подключиться к FTP-серверу по адресу *FTP.Microsoft.com*, введите:

```
open ftp.microsoft.com
```

Чтобы подключиться к FTP-серверу по адресу *FTP.Microsoft.com* , который прослушивает TCP-порт *755*, введите:

```
open ftp.microsoft.com 755
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
