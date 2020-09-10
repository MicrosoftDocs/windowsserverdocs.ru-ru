---
title: bitsadmin makecustomheaderswriteonly
description: Справочная статья по команде битсадмин макекустомхеадерсвритеонли, которая делает пользовательские заголовки HTTP для задания только для записи.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 0eee6cc2fd8c825f02f7e01750be743b10beb73e
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631482"
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
