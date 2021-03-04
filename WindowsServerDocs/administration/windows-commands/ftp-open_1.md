---
title: ftp open
description: Справочная статья по команде FTP Open, которая подключается к указанному FTP-серверу.
ms.topic: reference
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7770752d47d14f795b99f954b57a511bd439ec9b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817587"
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
