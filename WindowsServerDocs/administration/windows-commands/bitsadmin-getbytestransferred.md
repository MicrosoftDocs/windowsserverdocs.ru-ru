---
title: bitsadmin getbytestransferred
description: Справочная статья по команде битсадмин жетбитестрансферред, которая получает число байтов, переданных для указанного задания.
ms.topic: article
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1d6b8ebb8d03a2498796325de8878840f36c6b71
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894530"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred

Возвращает число байтов, переданных для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getbytestransferred <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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
