---
title: Задать контекст
description: Справочная статья по команде Set Context, которая задает контекст для создания теневой копии.
ms.topic: reference
ms.assetid: fc16c7dd-e8f0-4c2a-8742-0bddb2848bfd
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ce1414ab90f116f58618fcd67bc203f25dc58e46
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389098"
---
# <a name="set-context"></a>Задать контекст

Задает контекст для создания теневой копии. Если используется без параметров, **контекст Set** отображает справку в командной строке.

## <a name="syntax"></a>Синтаксис

```
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| клиентакцессибле | Указывает, что теневая копия может использоваться клиентскими версиями Windows. По умолчанию этот контекст является постоянным. |
| надежно | Указывает, что теневая копия сохраняется по выходу из программы, сбросу или перезапуску. |
| volatile | Удаляет теневую копию при выходе или сбросе. |
| средства записи | Указывает, что все модули записи исключены. |

## <a name="examples"></a>Примеры

Чтобы предотвратить удаление теневых копий при выходе из сценария DiskShadow, введите:

```
set context persistent
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда задания метаданных](set-metadata.md)

- [команда Set Option](set-option.md)

- [команда Set verbose](set-verbose.md)
