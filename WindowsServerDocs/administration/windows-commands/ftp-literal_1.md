---
title: ftp literal
description: Справочная статья по команде FTP Literal, которая отправляет точные аргументы на удаленный FTP-сервер.
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bafa2626481941b91d501e4fd6df52aa1f8f05d1
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889352"
---
# <a name="ftp-literal"></a>ftp literal

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отправляет точные аргументы на удаленный FTP-сервер. Возвращается один код ответа FTP.

> [!NOTE]
> Эта команда аналогична [команде FTP quote](ftp-quote.md).

## <a name="syntax"></a>Синтаксис

```
literal <argument> [ ]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<argument>` | Указывает аргумент для отправки на FTP-сервер. |

### <a name="examples"></a>Примеры

Чтобы отправить команду **Quit** на удаленный FTP-сервер, введите:

```
literal quit
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [FTP-команда в виде цитаты](ftp-quote.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
