---
title: bitsadmin gethttpmethod
description: Справочная статья по команде битсадмин жесттпмесод, которая получает команду HTTP для использования с заданием.
ms.topic: reference
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 41286885153ef6b06185d7934db12fe25cc6beda
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822076"
---
# <a name="bitsadmin-gethttpmethod"></a>bitsadmin gethttpmethod

Возвращает команду HTTP для использования с заданием.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /gethttpmethod <Job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
