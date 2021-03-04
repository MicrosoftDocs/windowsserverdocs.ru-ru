---
title: bitsadmin info
description: Справочная статья по команде битсадмин info, в которой отображаются сводные данные об указанном задании.
ms.topic: reference
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 06a26214660ce8e2b01b7dbb876f0128fd5a306b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821568"
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
