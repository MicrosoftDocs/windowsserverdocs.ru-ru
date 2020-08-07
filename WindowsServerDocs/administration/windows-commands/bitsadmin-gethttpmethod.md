---
title: bitsadmin gethttpmethod
description: Справочная статья по команде битсадмин жесттпмесод, которая получает команду HTTP для использования с заданием.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: ea6f1b3896b11bfcc157ea54dc0470786d3dff1f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894227"
---
# <a name="bitsadmin-gethttpmethod"></a>bitsadmin gethttpmethod

Возвращает команду HTTP для использования с заданием.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /gethttpmethod <Job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить команду HTTP для использования с заданием с именем *мидовнлоаджоб*:

```
bitsadmin /gethttpmethod myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
