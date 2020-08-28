---
title: bitsadmin makecustomheaderswriteonly
description: Справочная статья по команде битсадмин макекустомхеадерсвритеонли, которая делает пользовательские заголовки HTTP для задания только для записи.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 4d31f51c2531079342e223752c626b0b7e8d19f8
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024268"
---
# <a name="bitsadmin-makecustomheaderswriteonly"></a>bitsadmin makecustomheaderswriteonly

Сделайте пользовательские HTTP-заголовки задания только для записи.

> [!IMPORTANT]
> Это действие нельзя отменить.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /makecustomheaderswriteonly <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы сделать пользовательские заголовки HTTP только для записи для задания с именем *мидовнлоаджоб*, сделайте следующее:

```
bitsadmin /makecustomheaderswriteonly myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
