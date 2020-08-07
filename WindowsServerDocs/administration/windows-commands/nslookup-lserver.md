---
title: nslookup lserver
description: Справочная статья по команде nslookup лсервер, которая изменяет первоначальный сервер на указанный домен службы доменных имен (DNS).
ms.topic: article
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ab7c478b6c9f3ae299559a556629e53f9eb852ee
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885792"
---
# <a name="nslookup-lserver"></a>nslookup lserver

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет первоначальный сервер на указанный домен службы доменных имен (DNS).

Эта команда использует исходный сервер для поиска сведений об указанном домене DSN. Если необходимо выполнить поиск данных с использованием текущего сервера по умолчанию, используйте команду [nslookup Server](nslookup-server.md) .

## <a name="syntax"></a>Синтаксис

```
lserver <DNSdomain>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<DNSdomain>` | Указывает домен DNS для первоначального сервера. |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup server](nslookup-server.md)
