---
title: bitsadmin suspend
description: Справочная статья по команде битсадмин Suspend, которая приостанавливает указанное задание.
ms.topic: reference
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0827f7fe42a41d981c165e41b1a8af71ec5d7472
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630598"
---
# <a name="bitsadmin-suspend"></a>bitsadmin suspend

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Приостанавливает указанное задание. Если вы приостановили задание по ошибке, можно использовать параметр [возобновления битсадмин](bitsadmin-resume.md) , чтобы перезапустить задание.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /suspend <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
