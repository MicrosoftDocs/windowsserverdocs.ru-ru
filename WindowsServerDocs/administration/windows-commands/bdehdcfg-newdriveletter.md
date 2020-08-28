---
title: bdehdcfg newdriveletter
description: Справочная статья по команде BdeHdCfg невдривелеттер, которая назначает новую букву диска части диска, используемой в качестве системного диска.
ms.topic: reference
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf3cf52bfd23db5aadd82170de2bf20c8e602573
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031552"
---
# <a name="bdehdcfg-newdriveletter"></a>BdeHdCfg: невдривелеттер

Назначает новую букву диска части диска, используемой в качестве системного диска. Рекомендуется не назначать букву диска системному диску.

## <a name="syntax"></a>Синтаксис

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -newdriveletter <drive_letter>
```

#### <a name="parameters"></a>Параметры

| Параметр | Описание |
| ---------| ----------- |
| `<drive_letter>` | Определяет букву диска, которая будет назначена указанному целевому диску. |

## <a name="examples"></a>Примеры

Чтобы назначить диску по умолчанию букву диска, `P` сделайте следующее:

```
bdehdcfg -target default -newdriveletter P:
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
