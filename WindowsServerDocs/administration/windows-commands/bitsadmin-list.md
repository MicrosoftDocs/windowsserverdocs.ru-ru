---
title: bitsadmin list
description: Справочная статья по команде битсадмин List, в которой перечислены задания перемещения, принадлежащие текущему пользователю.
ms.topic: reference
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e1d36a9236c834cea76e653b9a2e639c3b8f964e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024378"
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
| /аллусерс | Необязательный элемент. Выводит список заданий для всех пользователей. Для использования этого параметра необходимо иметь права администратора. |
| /verbose | Необязательный элемент. Предоставляет подробные сведения о каждом задании. |

## <a name="examples"></a>Примеры

Для получения сведений о заданиях, принадлежащих текущему пользователю.

```
bitsadmin /list
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
