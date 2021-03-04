---
title: bitsadmin getfilestransferred
description: Справочная статья по команде битсадмин жетфилестрансферред, которая получает количество файлов, переданных для указанного задания.
ms.topic: reference
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4506828490004cfa5304e36c58446c5f7496822d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822038"
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
