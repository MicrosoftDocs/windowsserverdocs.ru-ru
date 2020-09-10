---
title: nslookup lserver
description: Справочная статья по команде nslookup лсервер, которая изменяет первоначальный сервер на указанный домен службы доменных имен (DNS).
ms.topic: reference
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d1f507b1a61e9fd4fc506fb4e74f869c83e95335
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635671"
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

| Параметр | Описание |
| --------- | ----------- |
| `<DNSdomain>` | Указывает домен DNS для первоначального сервера. |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup server](nslookup-server.md)
