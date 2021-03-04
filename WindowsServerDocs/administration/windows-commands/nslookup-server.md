---
title: nslookup server
description: Справочная статья по команде nslookup Server, которая изменяет сервер по умолчанию на указанный домен службы доменных имен (DNS).
ms.topic: reference
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bc523b0e7049fb55d8f246d6aa4b2be63ff9bf61
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101810178"
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
