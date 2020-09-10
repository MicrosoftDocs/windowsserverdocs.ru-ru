---
title: маска
description: Справочная статья по команде Mask, которая удаляет аппаратные теневые копии, импортированные с помощью команды Import.
ms.topic: reference
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ee0e4207a7c5cf6ad81ece39e9134881ad3c0239
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633718"
---
# <a name="mask"></a>маска

Удаляет аппаратные теневые копии, импортированные с помощью команды **Import** .

## <a name="syntax"></a>Синтаксис

```
mask <shadowsetID>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| шадовсетид | Удаляет теневые копии, принадлежащие указанному ИДЕНТИФИКАТОРу набора теневых копий. |

#### <a name="remarks"></a>Примечания

- Вместо *шадовсетид*можно использовать существующий псевдоним или переменную среды. Чтобы просмотреть существующие псевдонимы, используйте параметр **Добавить** без параметров.

### <a name="examples"></a>Примеры

Чтобы удалить импортированную теневую копию *% Import_1%*, введите:

```
mask %Import_1%
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)