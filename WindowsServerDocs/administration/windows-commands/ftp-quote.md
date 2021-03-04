---
title: ftp quote
description: Справочная статья по команде FTP quote, которая отправляет точные аргументы на удаленный FTP-сервер.
ms.topic: reference
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ab41deda18f6c9dd26e00b536ffd25ab8b6724b4
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817448"
---
# <a name="ftp-quote"></a>ftp quote

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отправляет точные аргументы на удаленный FTP-сервер. Возвращается один код ответа FTP.

> [!NOTE]
> Эта команда аналогична [команде FTP Literal](ftp-literal_1.md).

## <a name="syntax"></a>Синтаксис

```
quote <argument>[ ]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<argument>` | Указывает аргумент для отправки на FTP-сервер. |

### <a name="examples"></a>Примеры

Чтобы отправить команду **Quit** на удаленный FTP-сервер, введите:

```
quote quit
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Литеральная команда FTP](ftp-literal_1.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
