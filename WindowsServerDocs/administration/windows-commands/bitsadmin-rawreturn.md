---
title: bitsadmin rawreturn
description: Справочная статья по команде битсадмин равретурн, которая возвращает данные, подходящие для синтаксического анализа.
ms.topic: reference
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1d2be3712e4faf4803683ef32a10031894a913bd
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026442"
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
