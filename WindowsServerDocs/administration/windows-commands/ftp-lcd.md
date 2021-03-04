---
title: ftp lcd
description: Справочная статья по команде FTP LCD, которая изменяет рабочий каталог на локальном компьютере.
ms.topic: reference
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5988ec64b8f519604b093760cb684180f0069e52
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817708"
---
# <a name="ftp-lcd"></a>ftp lcd

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет рабочий каталог на локальном компьютере. По умолчанию рабочий каталог — это каталог, в котором была запущена команда **FTP** .

## <a name="syntax"></a>Синтаксис

```
lcd [<directory>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `[<directory>]` | Указывает каталог на локальном компьютере, который необходимо изменить. Если *Каталог* не указан, текущий рабочий каталог изменяется на каталог по умолчанию. |

### <a name="examples"></a>Примеры

Чтобы изменить рабочий каталог на локальном компьютере на *c:\Dir1*, введите:

```
lcd c:\dir1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
