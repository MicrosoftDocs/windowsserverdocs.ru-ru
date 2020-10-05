---
title: WDSUTIL Remove-дриверпаккаже
description: Справочная статья по WDSUTIL Remove-дриверпаккаже, которая удаляет пакет драйверов с сервера.
ms.topic: reference
ms.assetid: 6b201e91-0d44-4e4a-8252-8b0235df1002
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: fe40c9a1dbbf4a5f0bd09e61f39e6b9314a09337
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730628"
---
# <a name="wdsutil-remove-driverpackage"></a>WDSUTIL Remove-дриверпаккаже

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет пакет драйвера с сервера.

## <a name="syntax"></a>Синтаксис
```
wdsutil /remove-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
### <a name="parameters"></a>Параметры

|        Параметр        |                                                                            Описание                                                                             |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server: <Server name> ] |              Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.              |
| [/Дриверпаккаже: <Name> ] |                                                        Указывает имя удаляемого пакета драйверов.                                                         |
|    [/Паккажеид: <ID> ]    | Указывает идентификатор служб развертывания Windows для удаляемого пакета драйверов. Если пакет драйвера не может быть однозначно идентифицирован по имени, необходимо указать идентификатор. |

## <a name="examples"></a>Примеры
Чтобы просмотреть сведения об образах, введите одно из следующих действий:
```
wdsutil /remove-DriverPackage /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /remove-DriverPackage /Server:MyWdsServer /DriverPackage:MyDriverPackage
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Remove-дриверпаккажес](wdsutil-remove-driverpackages.md)
