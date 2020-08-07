---
title: маска
description: Справочная статья по команде Mask, которая удаляет аппаратные теневые копии, импортированные с помощью команды Import.
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a893d32dca90169d51a04db66b3dc796cbc69a46
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886527"
---
# <a name="mask"></a>маска

Удаляет аппаратные теневые копии, импортированные с помощью команды **Import** .

## <a name="syntax"></a>Синтаксис

```
mask <shadowsetID>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| шадовсетид | Удаляет теневые копии, принадлежащие указанному ИДЕНТИФИКАТОРу набора теневых копий. |

#### <a name="remarks"></a>Remarks

- Вместо *шадовсетид*можно использовать существующий псевдоним или переменную среды. Чтобы просмотреть существующие псевдонимы, используйте параметр **Добавить** без параметров.

### <a name="examples"></a>Примеры

Чтобы удалить импортированную теневую копию *% Import_1%*, введите:

```
mask %Import_1%
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)