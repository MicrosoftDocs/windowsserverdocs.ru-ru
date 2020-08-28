---
title: Get-Дриверпаккаже
description: Справочная статья по команде Get-Дриверпаккаже, которая отображает сведения о пакете драйверов на сервере.
ms.topic: reference
ms.assetid: 94d231e4-ff01-48e7-9bc8-7b0d97a4339e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 914effe6e2776f3bc66537beff5ea9e4bed65f3e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029672"
---
# <a name="get-driverpackage"></a>Get-Дриверпаккаже

Отображает сведения о пакете драйверов на сервере.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>Параметры

|        Параметр         |                                                                           Описание                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server: \<Server name> ] |              Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.               |
| [/Дриверпаккаже: \<Name> ] |                                                        Указывает имя пакета драйверов для отображения.                                                         |
|    [/Паккажеид: \<ID> ]    | Указывает идентификатор служб развертывания Windows для отображаемого пакета драйверов. Если пакет драйвера не может быть однозначно идентифицирован по имени, необходимо указать идентификатор. |
|     [/Show: {Drivers     |                                                                              Файлы                                                                               |

## <a name="examples"></a>Примеры

Чтобы просмотреть сведения о пакете драйвера, введите одно из следующих действий:
```
WDSUTIL /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)