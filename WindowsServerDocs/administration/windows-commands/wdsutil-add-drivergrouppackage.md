---
title: WDSUTIL Add-дриверграуппаккаже
description: Справочная статья по команде WDSUTIL Add-дриверграуппаккаже, которая добавляет пакет драйверов в группу драйверов.
ms.topic: reference
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7d478db93fb39eee6cc3e9f6a48df6690ef02ad5
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804167"
---
# <a name="wdsutil-add-drivergrouppackage"></a>WDSUTIL Add-дриверграуппаккаже

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет пакет драйверов в группу драйверов.

## <a name="syntax"></a>Синтаксис

```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /Дриверграуп:`<Groupname>` | Указывает имя новой группы драйверов. |
| Сервером`<Servername>` | Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
| /Дриверпаккаже:`<Name>` | Указывает имя пакета драйверов, добавляемого в группу. Этот параметр необходимо указать, если пакет драйверов не может быть однозначно идентифицирован по имени. |
| PackageId`<ID>` | Указывает идентификатор пакета. Чтобы найти идентификатор пакета, выберите группу драйверов, в которой находится пакет (или узел **все пакеты** ), щелкните правой кнопкой мыши пакет и выберите пункт **свойства**. Идентификатор пакета указан на вкладке **Общие** , например: **{DD098D20-1850-4fc8-8E35-EA24A1BEFF5E}**. |

## <a name="examples"></a>Примеры

Чтобы добавить пакет группы драйверов, введите:

```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```

```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /DriverPackage:XYZ
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Add-дриверграупфилтер](wdsutil-add-drivergroupfilter.md)

- [Команда WDSUTIL Add-дриверграуппаккажес](wdsutil-add-drivergrouppackages.md)

- [Команда WDSUTIL Add-дриверграуп](wdsutil-add-drivergroup.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
