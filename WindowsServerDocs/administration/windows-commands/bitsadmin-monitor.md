---
title: bitsadmin monitor
description: Справочная статья по команде монитора битсадмин, которая отслеживает задания в очереди на перемещение, принадлежащие текущему пользователю.
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3ba2cb315fb0696b8363506669aa41f1693bb758
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893666"
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
| /аллусерс | Необязательный элемент. Отслеживает задания для всех пользователей. Для использования этого параметра необходимо иметь права администратора. |
| /Refresh | Необязательный элемент. Обновляет данные через интервал, заданный параметром `<seconds>` . Интервал обновления по умолчанию составляет 5 секунд. Чтобы прервать обновление, нажмите клавиши CTRL + C. |

## <a name="examples"></a>Примеры

Для отслеживания очереди на перемещение заданий, принадлежащих текущему пользователю, и обновляет данные каждые 60 секунд.

```
bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
