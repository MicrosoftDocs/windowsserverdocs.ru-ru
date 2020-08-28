---
title: Get-Дриверграуп
description: Справочная статья по команде Get-Дриверграуп, которая отображает сведения о группах драйверов на сервере.
ms.topic: reference
ms.assetid: 7cfe10c3-a63f-48e7-bef9-f6b474b4ddbe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 545bf634382e562221438295e5d015f7dbb97bf3
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029682"
---
# <a name="get-drivergroup"></a>Get-Дриверграуп

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сведения о группах драйверов на сервере.

## <a name="syntax"></a>Синтаксис
```
wdsutil /Get-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|/Дриверграуп:<Group Name>|Указывает имя группы драйверов.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или FQDN.  Если имя сервера не указано, используется локальный сервер.|
|[/Show: {Паккажеметадата &#124; фильтры &#124; все}]|Отображает метаданные для всех пакетов драйверов в указанной группе. **Паккажеметадата** отображает сведения обо всех фильтрах для группы драйверов. **Фильтры** отображает метаданные для всех пакетов драйверов и фильтров для группы.|
## <a name="examples"></a>Примеры
Чтобы просмотреть сведения о файле драйвера, введите:
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Show:PackageMetaData
```
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Server:MyWdsServer /Show:Filters
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды Get-аллдриверграупс](using-the-get-alldrivergroups-command.md)
