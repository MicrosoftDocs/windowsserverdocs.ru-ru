---
title: Remove-Дриверграуппаккаже
description: Справочная статья по Remove-Дриверграуппаккаже, которая удаляет пакет драйверов из группы драйверов на сервере.
ms.topic: reference
ms.assetid: 2e48616d-d6a4-45f0-a5c6-efe62bf6a0ed
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e0f0aa02edbda29c3b1e14122687f0da0bb73685
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826503"
---
# <a name="remove-drivergrouppackage"></a>Remove-Дриверграуппаккаже



Удаляет пакет драйвера из группы драйверов на сервере.

## <a name="syntax"></a>Синтаксис

```
wdsutil /Remove-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|[/Server: \<Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.|
|[/Дриверпаккаже: \<Name> ]|Указывает имя удаляемого пакета драйверов.|
|[/Паккажеид: \<ID> ]|Указывает идентификатор служб развертывания Windows для удаляемого пакета драйверов. Этот параметр необходимо указать, если пакет драйверов не может быть однозначно идентифицирован по имени.|

## <a name="examples"></a>Примеры

```
wdsutil /Remove-DriverGroupPackage /DriverGroup:PrinterDrivers /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
wdsutil /Remove-DriverGroupPackage /DriverGroup:PrinterDrivers /DriverPackage:XYZ
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)