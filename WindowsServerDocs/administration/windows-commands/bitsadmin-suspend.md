---
title: bitsadmin suspend
description: Справочная статья по команде битсадмин Suspend, которая приостанавливает указанное задание.
ms.topic: article
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 90f6fcc9b28f75c51cdaf9c88ed61fbd1a3c2988
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881002"
---
# <a name="bitsadmin-suspend"></a>bitsadmin suspend

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Приостанавливает указанное задание. Если вы приостановили задание по ошибке, можно использовать параметр [возобновления битсадмин](bitsadmin-resume.md) , чтобы перезапустить задание.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /suspend <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ---------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="example"></a>Пример

Чтобы приостановить задание с именем *мидовнлоаджоб*:


```
bitsadmin /suspend myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда возобновления битсадмин](bitsadmin-resume.md)

- [Команда битсадмин](bitsadmin.md)
