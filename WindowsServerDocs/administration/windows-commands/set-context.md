---
title: Задать контекст
description: Справочная статья по параметру SET Context, который задает контекст для создания теневой копии.
ms.topic: article
ms.assetid: fc16c7dd-e8f0-4c2a-8742-0bddb2848bfd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3506a79ec713f26b16f58cd8cda3903ce6503adf
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882705"
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

## <a name="remarks"></a>Remarks

-   По умолчанию контекст *клиентакцессибле* является постоянным.

## <a name="examples"></a>Примеры

Чтобы предотвратить удаление теневых копий при выходе из сценария DiskShadow, введите:
```
set context persistent
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)