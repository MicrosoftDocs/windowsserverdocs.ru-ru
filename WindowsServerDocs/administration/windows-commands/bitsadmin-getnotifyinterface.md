---
title: bitsadmin getnotifyinterface
description: Справочная статья по команде битсадмин жетнотифинтерфаце, которая определяет, зарегистрировал ли другая программа интерфейс обратного вызова COM для указанного задания.
ms.topic: reference
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1455975083ac6afb25a02dc19c6df282928af587
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027812"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

Определяет, зарегистрировал ли другая программа интерфейс обратного вызова COM (интерфейс уведомления) для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getnotifyinterface <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

#### <a name="output"></a>Выходные данные

Выходные данные этой команды отображаются как, **зарегистрированные** или **отмененные**.

> [!NOTE]
> Невозможно определить программу, которая зарегистрировала интерфейс обратного вызова.

## <a name="examples"></a>Примеры

Чтобы получить интерфейс уведомления для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getnotifyinterface myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
