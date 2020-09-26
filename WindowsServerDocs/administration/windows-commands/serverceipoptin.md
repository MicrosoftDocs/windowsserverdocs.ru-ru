---
title: serverceipoptin
description: Справочная статья по серверцеипоптин, которая позволяет участвовать в программа улучшения качества программного обеспечения (CEIP).
ms.topic: reference
ms.assetid: 3d7d7fa7-0689-4797-b802-36fe260d21a0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6df387158a9630ab767dda655346836355fae936
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389172"
---
# <a name="serverceipoptin"></a>serverceipoptin

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Позволяет участвовать в программа улучшения качества программного обеспечения (CEIP).

## <a name="syntax"></a>Синтаксис

```
serverceipoptin [/query] [/enable] [/disable]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /Query | Проверяет текущее значение параметра. |
| разрешение | Включает участие в программе CEIP. |
| /Disable | Отключение участия в программе улучшения качества по. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы проверить текущие параметры, введите:

```
serverceipoptin /query
```

Чтобы включить участие, введите:

```
serverceipoptin /enable
```

Чтобы отключить участие, введите:

```
serverceipoptin /disable
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
