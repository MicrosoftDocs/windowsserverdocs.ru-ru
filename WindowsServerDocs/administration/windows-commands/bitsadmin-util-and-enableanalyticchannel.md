---
title: bitsadmin util и enableanalyticchannel
description: Справочная статья по команде битсадмин util and енаблеаналитикчаннел, которая включает или отключает канал аналитики клиента службы BITS.
ms.topic: reference
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 78fb63b135686e7cfee35f6247fd299d958f6b11
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820626"
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
