---
title: WDSUTIL Add-дриверграуппаккаже
description: Справочная статья по WDSUTIL Add-дриверграуппаккаже, которая добавляет пакет драйверов в группу драйверов.
ms.topic: reference
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9389bbf7421e8c41c32760b8a20d85c4e4b675ea
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91731098"
---
# <a name="wdsutil-add-drivergrouppackage"></a>WDSUTIL Add-дриверграуппаккаже

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет пакет драйверов в группу драйверов.

## <a name="syntax"></a>Синтаксис
```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```
### <a name="parameters"></a>Параметры

|         Параметр         |                                                                                                                                               Описание                                                                                                                                               |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Дриверграуп:<Group Name> |                                                                                                                                 Указывает имя группы драйверов.                                                                                                                                 |
|   Сервером<Server name>   |                                                                                  Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.                                                                                  |
|   /Дриверпаккаже:<Name>   |                                                                      Указывает имя пакета драйверов, добавляемого в группу. Этот параметр необходимо указать, если пакет драйверов не может быть однозначно идентифицирован по имени.                                                                       |
|      PackageId<ID>      | Указывает идентификатор пакета. Чтобы найти идентификатор пакета, щелкните группу драйверов, в которой находится пакет (или узел **все пакеты** ), щелкните правой кнопкой мыши пакет и выберите пункт **свойства**. Идентификатор пакета указан на вкладке **Общие** , например: **{DD098D20-1850-4fc8-8E35-EA24A1BEFF5E}**. |

## <a name="examples"></a>Примеры
Чтобы добавить пакет драйвера, введите один из следующих элементов:
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /DriverPackage:XYZ
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Add-дриверграуппаккажес](wdsutil-add-drivergrouppackages.md)
- [Команда WDSUTIL Add-дриверпаккаже](wdsutil-add-driverpackage.md)
- [Команда WDSUTIL Add-аллдриверпаккажес](wdsutil-add-alldriverpackages.md)
