---
title: bitsadmin gethttpmethod
description: Справочная статья по команде битсадмин жесттпмесод, которая получает команду HTTP для использования с заданием.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 5bbd2509cabea7ae68240a31cee78d9ffd3ac5e0
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033532"
---
# <a name="bitsadmin-gethttpmethod"></a>bitsadmin gethttpmethod

Возвращает команду HTTP для использования с заданием.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /gethttpmethod <Job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить команду HTTP для использования с заданием с именем *мидовнлоаджоб*:

```
bitsadmin /gethttpmethod myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
