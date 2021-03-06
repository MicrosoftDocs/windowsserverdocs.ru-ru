---
title: WDSUTIL Get-аллдриверграупс
description: Справочная статья по команде WDSUTIL Get-аллдриверграупс, которая отображает сведения обо всех группах драйверов на сервере.
ms.topic: reference
ms.assetid: f245ba53-f150-41b1-8418-38dcf0410a05
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4fdcb5b271a118622a6fe4dea60bf6225f6f4b36
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101803749"
---
# <a name="wdsutil-get-alldrivergroups"></a>WDSUTIL Get-аллдриверграупс

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сведения обо всех группах драйверов на сервере.

## <a name="syntax"></a>Синтаксис

```
wdsutil /get-alldrivergroups [/server:<servername>] [/show:{packagemetadata | filters | all}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `[/server:<servername>]` | Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
| `/show:{packagemetadata | filters | all}]` | Отображает метаданные для всех пакетов драйверов в указанной группе. **Паккажеметадата** отображает сведения обо всех фильтрах для группы драйверов. **Фильтры** отображает метаданные для всех пакетов драйверов и фильтров для группы. |

## <a name="examples"></a>Примеры

Чтобы просмотреть сведения о файле драйвера, введите:

```
wdsutil /get-alldrivergroups /server:MyWdsServer /show:All
```

```
wdsutil /get-alldrivergroups [/show:packagemetadata]
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
-
- [Команда WDSUTIL Get-дриверграуп](wdsutil-get-drivergroup.md)
