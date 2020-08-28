---
title: nslookup root
description: Справочная статья по команде nslookup root, которая изменяет сервер по умолчанию на сервер для корневого каталога пространства имен домена системы доменных имен (DNS).
ms.topic: reference
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ef505427e92b6f0e14adf92d9eea463feb582314
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038795"
---
# <a name="nslookup-root"></a>nslookup root

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет сервер по умолчанию на сервер для корня пространства имен домена службы доменных имен (DNS). В настоящее время используется сервер имен ns.nic.ddn.mil. Имя корневого сервера можно изменить с помощью команды [nslookup set root](nslookup-set-root.md) .

> [!NOTE]
> Эта команда совпадает с `lserver ns.nic.ddn.mil` .

## <a name="syntax"></a>Синтаксис

```
root
```

### <a name="parameters"></a>Параметры

| Параметр | Description |
| --------- | ----------- |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup set root](nslookup-set-root.md)
