---
title: bitsadmin setminretrydelay
description: Справочная статья по команде битсадмин сетминретриделай, которая задает минимальный интервал времени (в секундах), в течение которого BITS ожидает после возникновения временной ошибки, прежде чем пытаться переместить файл.
ms.topic: reference
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9bb194ff9a347d5e2a2caadeb22cf94f6a8fa9c1
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820868"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

Задает минимальное время в секундах, в течение которого BITS ожидает после возникновения временной ошибки, прежде чем пытаться переместить файл.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setminretrydelay <job> <retrydelay>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| retrydelay | Минимальное время ожидания BITS после ошибки во время передачи в секундах. |

## <a name="examples"></a>Примеры

Чтобы задать минимальную задержку повторных попыток в 35 секунд для задания с именем *мидовнлоаджоб*:

```
bitsadmin /setminretrydelay myDownloadJob 35
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
