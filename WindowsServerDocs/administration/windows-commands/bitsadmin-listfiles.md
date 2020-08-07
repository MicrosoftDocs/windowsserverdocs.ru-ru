---
title: bitsadmin listfiles
description: Справочная статья по команде битсадмин листфилес, в которой перечислены файлы в указанном задании.
ms.topic: article
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a5dcd9092f2d9a8d150496e4cf89595537885d62
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893687"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles

Перечисляет файлы в указанном задании.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /listfiles <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить список файлов для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /listfiles myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
