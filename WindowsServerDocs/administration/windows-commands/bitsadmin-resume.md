---
title: bitsadmin resume
description: Справочная статья по команде битсадмин Resume, которая активирует новое или приостановленное задание в очереди на перемещение.
ms.topic: reference
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3bd2563232041306ec74a3890bcad8cd4c854fc2
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821168"
---
# <a name="bitsadmin-resume"></a>bitsadmin resume

Активирует новое или приостановленное задание в очереди на перемещение. Если вы возобновили задание по ошибке или просто хотите приостановить задание, можно использовать параметр [Suspend битсадмин](bitsadmin-suspend.md) для приостановки задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /resume <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы возобновить задание с именем *мидовнлоаджоб*:

```
bitsadmin /resume myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [битсадмин Suspend, команда](bitsadmin-suspend.md)

- [Команда битсадмин](bitsadmin.md)
