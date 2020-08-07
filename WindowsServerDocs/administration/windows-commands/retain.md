---
title: retain
description: Справочная статья для * * * *-
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a0205f3b67bd99ca590c7ffc6fbd04b0eefd94f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883647"
---
# <a name="retain"></a>retain



Подготавливает существующий динамический простой том для использования в качестве загрузочного или системного тома.

## <a name="syntax"></a>Синтаксис

```
retain
```

## <a name="remarks"></a>Remarks

-   На динамическом диске с основной загрузочной записью эта команда создает запись раздела в основной загрузочной записи.
-   На динамическом диске с таблицей разделов GPT эта команда создает запись секции в таблице разделов GUID.

## <a name="additional-references"></a>Дополнительные ссылки

