---
title: ftp quote
description: Справочная статья по команде FTP quote, которая отправляет точные аргументы на удаленный FTP-сервер.
ms.topic: reference
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e70c93e7a8fe5c32038eec08c7115aa1fec80bf
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035802"
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
