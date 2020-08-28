---
title: bitsadmin info
description: Справочная статья по команде битсадмин info, в которой отображаются сводные данные об указанном задании.
ms.topic: reference
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a909655215d73b1fd197155810b980d5aaa04eab
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028572"
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
| /verbose | Необязательный элемент. Предоставляет подробные сведения о каждом задании. |

## <a name="examples"></a>Примеры

Для получения сведений о задании с именем *мидовнлоаджоб*:

```
bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)
