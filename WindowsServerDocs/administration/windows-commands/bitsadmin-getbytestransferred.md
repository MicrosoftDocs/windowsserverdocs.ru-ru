---
title: bitsadmin getbytestransferred
description: Справочная статья по команде битсадмин жетбитестрансферред, которая получает число байтов, переданных для указанного задания.
ms.topic: reference
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c0b8db1e093f144a2480294dc4ce4673cbaf33dd
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822228"
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
