---
title: bitsadmin resume
description: Справочная статья по команде битсадмин Resume, которая активирует новое или приостановленное задание в очереди на перемещение.
ms.topic: reference
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbbd4f322f416dd76e9c2fca6e3539f199ac1ed6
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026312"
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
