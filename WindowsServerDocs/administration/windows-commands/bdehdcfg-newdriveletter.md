---
title: bdehdcfg newdriveletter
description: Справочная статья по команде BdeHdCfg невдривелеттер, которая назначает новую букву диска части диска, используемой в качестве системного диска.
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b13bae914f06af4b282ed558384c9cdc14f5bc11
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895110"
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
