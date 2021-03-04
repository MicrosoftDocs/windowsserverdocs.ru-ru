---
title: bitsadmin list
description: Справочная статья по команде битсадмин List, в которой перечислены задания перемещения, принадлежащие текущему пользователю.
ms.topic: reference
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 40e7492ea44b23b0093b9a124a1e4f238ee9419b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821478"
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
