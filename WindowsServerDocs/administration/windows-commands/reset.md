---
title: сброс
description: Справочная статья для * * * *-
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f491a3d8c805ac6b3558f3778f6eba91a7551b82
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883655"
---
# <a name="reset"></a>сброс



Сбрасывает DiskShadow.exe в состояние по умолчанию. **Reset** особенно полезен при разделении составных операций DiskShadow, таких как **Создание**, **Импорт**, **резервное копирование**или **Восстановление**.

## <a name="syntax"></a>Синтаксис

```
reset
```

## <a name="remarks"></a>Remarks

-   При использовании команды **Reset** состояние теряется из таких команд, как **Add**, **Set**, **Load**или **Writer**. **Сброс** также освобождает ивссбаккупкомпонент интерфейсы и теряет непостоянные теневые копии.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)