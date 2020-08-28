---
title: bitsadmin getvalidationstate
description: Справочная статья по команде битсадмин жетвалидатионстате, которая сообщает состояние проверки содержимого заданного файла в задании.
ms.topic: reference
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 173bbaad6508ec3ae8100232fda598fe7a422296
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028642"
---
# <a name="bitsadmin-getvalidationstate"></a>bitsadmin getvalidationstate

Сообщает состояние проверки содержимого заданного файла в задании.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getvalidationstate <job> <file_index>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| file_index | Начинается с 0. |

## <a name="examples"></a>Примеры

Чтобы получить состояние проверки содержимого файла 2 в задании с именем *мидовнлоаджоб*:

```
bitsadmin /getvalidationstate myDownloadJob 1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
