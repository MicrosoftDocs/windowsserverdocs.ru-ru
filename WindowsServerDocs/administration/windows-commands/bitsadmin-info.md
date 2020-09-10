---
title: bitsadmin info
description: Справочная статья по команде битсадмин info, в которой отображаются сводные данные об указанном задании.
ms.topic: reference
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 815fdc719d584f7d25f88705056e4d5c0c3405aa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631532"
---
# <a name="bitsadmin-info"></a>bitsadmin info

Отображает сводную информацию об указанном задании.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /info <job> [/verbose]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| /verbose | Необязательный параметр. Предоставляет подробные сведения о каждом задании. |

## <a name="examples"></a>Примеры

Для получения сведений о задании с именем *мидовнлоаджоб*:

```
bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)
