---
title: help
description: Справочная статья по команде Help, в которой отображается список доступных команд или подробные справочные сведения об указанной команде.
ms.topic: reference
ms.assetid: c65b5ac3-711a-4368-95b8-ba82e2d00713
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ac651769082b5df65b29bc7c86b6129a097b8c84
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101816590"
---
# <a name="help"></a>help

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает список доступных команд или подробные справочные сведения об указанной команде. Если используется без параметров, **Справочные** списки и краткое описание каждой системной команды.

## <a name="syntax"></a>Синтаксис

```
help [<command>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<command>` | Указывает команду, для которой отображаются подробные справочные сведения. |

### <a name="examples"></a>Примеры

Чтобы просмотреть сведения о команде **Robocopy** , введите:

```
help robocopy
```

Чтобы отобразить список всех команд, доступных в DiskPart, введите:

```
help
```

Чтобы просмотреть подробные справочные сведения о том, как использовать команду **создать секцию** в DiskPart, введите:

```
help create partition primary
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
