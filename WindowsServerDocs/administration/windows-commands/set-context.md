---
title: Задать контекст
description: Справочная статья по параметру SET Context, который задает контекст для создания теневой копии.
ms.topic: reference
ms.assetid: fc16c7dd-e8f0-4c2a-8742-0bddb2848bfd
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7c89c0da8b63cef5b534163c5dbc1a0bee0cddbf
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637754"
---
# <a name="set-contex"></a>Задать контекста

Задает контекст для создания теневой копии. Если используется без параметров, **контекст Set** отображает справку в командной строке.



## <a name="syntax"></a>Синтаксис

```
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|клиентакцессибле|Указывает, что теневая копия может использоваться клиентскими версиями Windows.|
|надежно|Указывает, что теневая копия сохраняется по выходу из программы, сбросу или перезапуску.|
|volatile|Удаляет теневую копию при выходе или сбросе.|
|средства записи|Указывает, что все модули записи исключены.|

## <a name="remarks"></a>Примечания

-   По умолчанию контекст *клиентакцессибле* является постоянным.

## <a name="examples"></a>Примеры

Чтобы предотвратить удаление теневых копий при выходе из сценария DiskShadow, введите:
```
set context persistent
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)