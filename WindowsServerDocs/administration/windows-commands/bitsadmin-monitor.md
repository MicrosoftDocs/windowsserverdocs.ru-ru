---
title: bitsadmin monitor
description: Справочная статья по команде монитора битсадмин, которая отслеживает задания в очереди на перемещение, принадлежащие текущему пользователю.
ms.topic: reference
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2245d9e4375130877755f96eed42a46a479742f3
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631474"
---
# <a name="bitsadmin-monitor"></a>bitsadmin monitor

Отслеживает задания в очереди на перемещение, принадлежащие текущему пользователю.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /monitor [/allusers] [/refresh <seconds>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| /аллусерс | Необязательный параметр. Отслеживает задания для всех пользователей. Для использования этого параметра необходимо иметь права администратора. |
| /Refresh | Необязательный параметр. Обновляет данные через интервал, заданный параметром `<seconds>` . Интервал обновления по умолчанию составляет 5 секунд. Чтобы прервать обновление, нажмите клавиши CTRL + C. |

## <a name="examples"></a>Примеры

Для отслеживания очереди на перемещение заданий, принадлежащих текущему пользователю, и обновляет данные каждые 60 секунд.

```
bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
