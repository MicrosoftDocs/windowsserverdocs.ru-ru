---
title: nslookup lserver
description: Справочная статья по команде nslookup лсервер, которая изменяет первоначальный сервер на указанный домен службы доменных имен (DNS).
ms.topic: reference
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bf7729dd0d61b3895f6d5d44d35d89b7b9150119
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101810391"
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
