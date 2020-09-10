---
title: bitsadmin getfilestransferred
description: Справочная статья по команде битсадмин жетфилестрансферред, которая получает количество файлов, переданных для указанного задания.
ms.topic: reference
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b4a34e799b2d7e41373a1b4682c77e3ad93d36c2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632097"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred

Возвращает количество файлов, переданных для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getfilestransferred <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить количество файлов, переданных в задании с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getfilestransferred myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
