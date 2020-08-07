---
title: bitsadmin cancel
description: Справочная статья по команде битсадмин Cancel, которая удаляет задание из очереди на перемещение и удаляет все временные файлы, связанные с заданием.
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 603a398aef42052e25828b917748ed2b10287620
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894650"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

Удаляет задание из очереди на перемещение и удаляет все временные файлы, связанные с заданием.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /cancel <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы удалить задание *мидовнлоаджоб* из очереди обмена:

```
bitsadmin /cancel myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
