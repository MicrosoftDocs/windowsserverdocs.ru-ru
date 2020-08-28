---
title: bitsadmin getbytestransferred
description: Справочная статья по команде битсадмин жетбитестрансферред, которая получает число байтов, переданных для указанного задания.
ms.topic: reference
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67e1432f2fbef32ac47320d87993f5d62053bb71
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028742"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred

Возвращает число байтов, переданных для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getbytestransferred <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить число байтов, передаваемых для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getbytestransferred myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
