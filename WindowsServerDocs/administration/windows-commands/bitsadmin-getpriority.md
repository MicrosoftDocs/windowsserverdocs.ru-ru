---
title: bitsadmin getpriority
description: Справочная статья по команде битсадмин предшествовал, которая получает приоритет указанного задания.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 397a762a210aeae7a02e49283330a2d4214876e6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631768"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

Возвращает приоритет указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getpriority <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

#### <a name="output"></a>Выходные данные

Для этой команды может быть возвращен следующий приоритет:

- **ПЕРЕДНЕГО плана**

- **ВЫСОКОМ**

- **ОБЫЧНО**

- **НИЗШУЮ**

- **UNKNOWN**

## <a name="examples"></a>Примеры

Чтобы получить приоритет для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
