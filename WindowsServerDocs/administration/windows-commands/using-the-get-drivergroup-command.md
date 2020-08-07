---
title: Get-Дриверграуп
description: Справочная статья по команде Get-Дриверграуп, которая отображает сведения о группах драйверов на сервере.
ms.topic: article
ms.assetid: 7cfe10c3-a63f-48e7-bef9-f6b474b4ddbe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 95981c1821117f6a4a634df001b901ee76816b75
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896960"
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
