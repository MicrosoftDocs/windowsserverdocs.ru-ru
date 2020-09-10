---
title: битсадмин жетпроксилист — извлекает список прокси-серверов для указанного задания.
description: Справочная статья по команде битсадмин жетпроксилист, которая получает список прокси-серверов для указанного задания.
ms.topic: reference
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4d4cefcb27a9aa18b06bc588d08aba2f2f810636
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631741"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

Извлекает разделенный запятыми список прокси-серверов, используемых для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getproxylist <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить список прокси-серверов для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getproxylist myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
