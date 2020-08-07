---
title: bitsadmin getnotifyinterface
description: Справочная статья по команде битсадмин жетнотифинтерфаце, которая определяет, зарегистрировал ли другая программа интерфейс обратного вызова COM для указанного задания.
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0e22b240f16aa417cf46b715527cd9098c60794
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894063"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

Определяет, зарегистрировал ли другая программа интерфейс обратного вызова COM (интерфейс уведомления) для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getnotifyinterface <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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
