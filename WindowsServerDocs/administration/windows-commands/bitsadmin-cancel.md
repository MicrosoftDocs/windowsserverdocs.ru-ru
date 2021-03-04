---
title: bitsadmin cancel
description: Справочная статья по команде битсадмин Cancel, которая удаляет задание из очереди на перемещение и удаляет все временные файлы, связанные с заданием.
ms.topic: reference
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b45c12403327f097be32eefd673b1ff8235ecd21
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822378"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

Удаляет задание из очереди на перемещение и удаляет все временные файлы, связанные с заданием.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /cancel <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
