---
title: serverceipoptin
description: Справочная статья для * * * *-
ms.topic: reference
ms.assetid: 3d7d7fa7-0689-4797-b802-36fe260d21a0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 25a7b116387af973a8c7894edbd0daed0dc59f9a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024968"
---
# <a name="serverceipoptin"></a>serverceipoptin

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Позволяет участвовать в программа улучшения качества программного обеспечения (CEIP).
## <a name="syntax"></a>Синтаксис
```
serverceipoptin [/query] [/enable] [/disable]
```
#### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|/Query|проверяет текущее значение параметра.|
|разрешение|Включает участие.|
|/Disable|Отключает участие.|
|/?|Отображение справки в командной строке.|
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

