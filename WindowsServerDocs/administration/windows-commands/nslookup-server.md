---
title: nslookup server
description: Справочная статья по команде nslookup Server, которая изменяет сервер по умолчанию на указанный домен службы доменных имен (DNS).
ms.topic: reference
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 64d1383dd5c4fa86a62fad91bae0ed5e4eb1454b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635628"
---
# <a name="nslookup-server"></a>nslookup server

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет сервер по умолчанию на указанный домен службы доменных имен (DNS).

Эта команда использует текущий сервер по умолчанию для поиска сведений об указанном домене DSN. Если вы хотите найти информацию с помощью начального сервера, используйте команду [nslookup лсервер](nslookup-lserver.md) .

## <a name="syntax"></a>Синтаксис

```
server <DNSdomain>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<DNSdomain>` | Указывает домен DNS для сервера по умолчанию. |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup lserver](nslookup-lserver.md)
