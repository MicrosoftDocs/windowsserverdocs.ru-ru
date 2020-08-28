---
title: bitsadmin setminretrydelay
description: Справочная статья по команде битсадмин сетминретриделай, которая задает минимальный интервал времени (в секундах), в течение которого BITS ожидает после возникновения временной ошибки, прежде чем пытаться переместить файл.
ms.topic: reference
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ef8ed52e991ae9c2d1807ade604cc0cab066743
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031272"
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
