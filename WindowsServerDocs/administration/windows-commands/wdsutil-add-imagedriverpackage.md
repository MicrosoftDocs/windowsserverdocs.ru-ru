---
title: WDSUTIL Add-имажедриверпаккаже
description: Справочная статья по команде WDSUTIL Add-имажедриверпаккаже, которая добавляет пакет драйверов, который находится в хранилище драйверов, в существующий образ загрузки на сервере.
ms.topic: reference
ms.assetid: 6c2a4833-6427-47f8-9ffb-20b3786cb406
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d1f84bcc7715969da6964bca82c15a5f8a39040f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804147"
---
# <a name="wdsutil-add-imagedriverpackage"></a>WDSUTIL Add-имажедриверпаккаже

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет пакет драйверов, который находится в хранилище драйверов, в существующий образ загрузки на сервере.

## <a name="syntax"></a>Синтаксис

```
wdsutil /add-ImageDriverPackage [/Server:<Servername>] [media:<Imagename>] [mediatype:Boot] [/Architecture:{x86 | ia64 | x64}] [/Filename:<Filename>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер. |
| [носитель: `<Imagename>` ] | Указывает имя образа, в который добавляется драйвер. |
| [MediaType: Boot] | Указывает тип образа, в который добавляется драйвер. Пакеты драйверов можно добавлять только в загрузочные образы. |
| [/Арчитектуре: `{x86 | ia64 | x64}` ] | Указывает архитектуру загрузочного образа. Так как для образов загрузки можно использовать одно и то же имя образа в разных архитектурах, следует указать архитектуру для обеспечения правильного использования образа. |
| [/Филенаме: `<Filename>` ] | Указывает имя файла. Если образ не может быть однозначно определен по имени, необходимо указать имя файла. |
| [/Дриверпаккаже:`<Name>` | Указывает имя пакета драйверов, добавляемого к образу. |
| [/Паккажеид: `<ID>` ] | Указывает идентификатор служб развертывания Windows для пакета драйверов. Этот параметр необходимо указать, если пакет драйверов не может быть однозначно идентифицирован по имени. Чтобы найти идентификатор пакета, выберите группу драйверов, в которой находится пакет (или узел **все пакеты** ), щелкните правой кнопкой мыши пакет и выберите пункт **свойства**. Идентификатор пакета указан на вкладке **Общие** . Например: {DD098D20-1850-4fc8-8E35-EA24A1BEFF5E}. |

## <a name="examples"></a>Примеры

Чтобы добавить пакет драйверов в загрузочный образ, введите:

```
wdsutil /add-ImageDriverPackagmedia:WinPE Boot Imagemediatype:Boot /Architecture:x86 /DriverPackage:XYZ
```

```
wdsutil /verbose /add-ImageDriverPackagmedia:WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Add-имажедриверпаккажес](wdsutil-add-imagedriverpackages.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
