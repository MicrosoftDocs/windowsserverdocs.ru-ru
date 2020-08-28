---
title: bitsadmin getpriority
description: Справочная статья по команде битсадмин предшествовал, которая получает приоритет указанного задания.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 2aeff973b0ca285cc8c9852f284e314879f8de02
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028702"
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

- **HIGH.**

- **ОБЫЧНО**

- **LOW**

- **UNKNOWN**

## <a name="examples"></a>Примеры

Чтобы получить приоритет для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
