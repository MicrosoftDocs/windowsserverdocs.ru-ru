---
title: serverceipoptin
description: Справочная статья по серверцеипоптин, которая позволяет участвовать в программа улучшения качества программного обеспечения (CEIP).
ms.topic: reference
ms.assetid: 3d7d7fa7-0689-4797-b802-36fe260d21a0
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f1bb7e747ff45fcffa0a6454312f70e3170014ed
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805987"
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
