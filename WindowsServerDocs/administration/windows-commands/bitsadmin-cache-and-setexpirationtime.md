---
title: bitsadmin cache и setexpirationtime
description: Справочная статья по битсадмин кэшу и команде сетекспиратионтиме, которая задает срок действия кэша.
ms.topic: article
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 367088525366707797296d844f134dcf8a02def7
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894734"
---
# <a name="bitsadmin-cache-and-setexpirationtime"></a>bitsadmin cache и setexpirationtime

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Задает срок действия кэша.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /cache /setexpirationtime secs
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| сек | Количество секунд до истечения срока действия кэша. |

## <a name="examples"></a>Примеры

Чтобы задать срок действия кэша через 60 секунд:

```
bitsadmin /cache / setexpirationtime 60
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда кэша битсадмин](bitsadmin-cache.md)
