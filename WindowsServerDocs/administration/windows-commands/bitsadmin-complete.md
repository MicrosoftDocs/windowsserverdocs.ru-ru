---
title: bitsadmin complete
description: Справочная статья по команде битсадмин Complete, которая завершает задание.
ms.topic: reference
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 88e8ac3920adb80dcc453317fbffe5fd661811fb
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632385"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

Завершает задание. Используйте этот параметр после перемещения задания в состояние "передано". В противном случае будут доступны только те файлы, которые были успешно переданы.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /complete <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
