---
title: bitsadmin complete
description: Справочная статья по команде битсадмин Complete, которая завершает задание.
ms.topic: article
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 43c3296520b5843643c10d204d89f4f2f2bf98d8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894609"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

Завершает задание. Используйте этот параметр после перемещения задания в состояние "передано". В противном случае будут доступны только те файлы, которые были успешно переданы.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /complete <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="example"></a>Пример

Чтобы завершить задание *мидовнлоаджоб* , после достижения `TRANSFERRED` состояния выполните следующие действия.

```
bitsadmin /complete myDownloadJob
```

Если несколько заданий используют *мидовнлоаджоб* в качестве имени, необходимо использовать идентификатор GUID задания, чтобы однозначно идентифицировать его для завершения.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
