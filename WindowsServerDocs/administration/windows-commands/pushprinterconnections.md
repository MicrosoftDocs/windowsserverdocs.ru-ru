---
title: pushprinterconnections
description: Справочная статья по команде PushPrinterConnections, которая считывает развернутые параметры подключения принтера из групповая политика и развертывает и удаляет подключения принтеров по мере необходимости.
ms.topic: reference
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dc918536d6814bbbd6a61d9d59479ab0b0bbaadf
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101807843"
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
| > < журнала | Записывает файл журнала отладки на пользователя в *% TEMP* или записывает журнал отладки на компьютер в *%виндир%\темп*. |
| <-? > | Отображает справку в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Справочник по командам системы печати](print-command-reference.md)

- [Развертывание принтеров с помощью групповая политика](https://go.microsoft.com/fwlink/?LinkId=230627)
