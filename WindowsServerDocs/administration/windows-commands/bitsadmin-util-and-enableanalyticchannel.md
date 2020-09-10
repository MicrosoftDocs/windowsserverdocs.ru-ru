---
title: bitsadmin util и enableanalyticchannel
description: Справочная статья по команде битсадмин util and енаблеаналитикчаннел, которая включает или отключает канал аналитики клиента службы BITS.
ms.topic: reference
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 391b53694fcb21d1c17085d487908b090ad88f0a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630561"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util и enableanalyticchannel

Включает или отключает аналитический канал клиента BITS.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /util /enableanalyticchannel TRUE|FALSE
```

| Параметр | Описание |
| --------- | ---------- |
| TRUE или FALSE | **Значение true** включает проверку содержимого для указанного файла, а **значение false** отключает его. |

## <a name="examples"></a>Примеры

Для включения или отключения аналитического канала клиента BITS.

```
bitsadmin /util / enableanalyticchannel TRUE
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [битсадмин util, команда](bitsadmin-util.md)

- [Команда битсадмин](bitsadmin.md)
