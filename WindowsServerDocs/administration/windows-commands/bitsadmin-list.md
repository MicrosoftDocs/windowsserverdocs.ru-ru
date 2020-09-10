---
title: bitsadmin list
description: Справочная статья по команде битсадмин List, в которой перечислены задания перемещения, принадлежащие текущему пользователю.
ms.topic: reference
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 81fecf15f16cfa28933b63f9de693ba4e07679e8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631504"
---
# <a name="bitsadmin-list"></a>bitsadmin list

Список заданий перемещения, принадлежащих текущему пользователю.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /list [/allusers][/verbose]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| /аллусерс | Необязательный параметр. Выводит список заданий для всех пользователей. Для использования этого параметра необходимо иметь права администратора. |
| /verbose | Необязательный параметр. Предоставляет подробные сведения о каждом задании. |

## <a name="examples"></a>Примеры

Для получения сведений о заданиях, принадлежащих текущему пользователю.

```
bitsadmin /list
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
