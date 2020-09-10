---
title: nslookup root
description: Справочная статья по команде nslookup root, которая изменяет сервер по умолчанию на сервер для корневого каталога пространства имен домена системы доменных имен (DNS).
ms.topic: reference
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2e3dbbdf970143ce1e82f0c817fc1f53c5b22749
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635658"
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
