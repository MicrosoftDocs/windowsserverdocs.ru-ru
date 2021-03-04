---
title: WDSUTIL Remove-дриверпаккаже
description: Справочная статья по WDSUTIL Remove-дриверпаккаже, которая удаляет пакет драйверов с сервера.
ms.topic: reference
ms.assetid: 6b201e91-0d44-4e4a-8252-8b0235df1002
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5bba6969fcb0704db56cba2ca0a557e9e3d199ea
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825531"
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
