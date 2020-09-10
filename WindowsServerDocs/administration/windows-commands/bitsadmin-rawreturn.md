---
title: bitsadmin rawreturn
description: Справочная статья по команде битсадмин равретурн, которая возвращает данные, подходящие для синтаксического анализа.
ms.topic: reference
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 286e84c16087cc000a6af29b3be53d529425dfde
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631218"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

Возвращает данные, подходящие для синтаксического анализа. Как правило, эта команда используется совместно с параметрами **/CREATE** и **/Get*** для получения только значения. Этот параметр необходимо указать перед другими коммутаторами.

> [!NOTE]
> Эта команда удаляет символы новой строки и форматирование из выходных данных.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /rawreturn
```

## <a name="examples"></a>Примеры

Чтобы получить необработанные данные для состояния задания с именем *мидовнлоаджоб*:

```
bitsadmin /rawreturn /getstate myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
