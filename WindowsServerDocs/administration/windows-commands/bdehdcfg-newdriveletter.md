---
title: bdehdcfg newdriveletter
description: Справочная статья по команде BdeHdCfg невдривелеттер, которая назначает новую букву диска части диска, используемой в качестве системного диска.
ms.topic: reference
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c1e1bd6291808ef28e14309307cfd240fd0f8535
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822818"
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
