---
title: pushprinterconnections
description: Справочная статья по команде PushPrinterConnections, которая считывает развернутые параметры подключения принтера из групповая политика и развертывает и удаляет подключения принтеров по мере необходимости.
ms.topic: reference
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ef1cfc110d446da461251b9c7e28a4595edee291
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639933"
---
# <a name="pushprinterconnections"></a>pushprinterconnections

Считывает развернутые параметры подключения принтера из групповая политика и развертывает и удаляет подключения принтеров по мере необходимости.

> [!IMPORTANT]
> Эта служебная программа предназначена для использования при запуске компьютера или в сценариях входа пользователя, и не должна запускаться из командной строки.

## <a name="syntax"></a>Синтаксис

```
pushprinterconnections <-log> <-?>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| > < журнала | Записывает файл журнала отладки на пользователя в *% TEMP*или записывает журнал отладки на компьютер в *%виндир%\темп*. |
| <-? > | Отображает справку в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Справочник по командам системы печати](print-command-reference.md)

- [Развертывание принтеров с помощью групповая политика](https://go.microsoft.com/fwlink/?LinkId=230627)
