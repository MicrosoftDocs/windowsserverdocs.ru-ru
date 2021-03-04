---
title: bitsadmin getnotifyinterface
description: Справочная статья по команде битсадмин жетнотифинтерфаце, которая определяет, зарегистрировал ли другая программа интерфейс обратного вызова COM для указанного задания.
ms.topic: reference
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9a15feddbc0ab3483a5568c19bd68bf68ce7309a
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821838"
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
