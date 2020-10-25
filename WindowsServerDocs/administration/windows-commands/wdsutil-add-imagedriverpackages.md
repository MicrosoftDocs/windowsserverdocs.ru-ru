---
title: WDSUTIL Add-имажедриверпаккажес
description: Справочная статья по команде WDSUTIL Add-имажедриверпаккажес, которая добавляет пакеты драйверов из хранилища драйверов в загрузочный образ.
ms.topic: reference
ms.assetid: 9dc78909-a4d1-42a2-af8f-21ebcbfe8302
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 74029ca7b2243603c832b74f59a9248353cea911
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524479"
---
# <a name="wdsutil-add-imagedriverpackages"></a>WDSUTIL Add-имажедриверпаккажес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет пакеты драйверов из хранилища драйверов в загрузочный образ.

## <a name="syntax"></a>Синтаксис

```
wdsutil /add-ImageDriverPackages [/Server:<Server name>media:<Image namemediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>] /Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value> ...]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер. |
| [носитель: `<Imagename>` ] | Указывает имя образа, в который добавляется драйвер. |
| [MediaType: Boot] | Указывает тип образа, в который добавляется драйвер. Пакеты драйверов можно добавлять только в загрузочные образы. |
| [/Арчитектуре: `{x86 | ia64 | x64}` ] | Указывает архитектуру загрузочного образа. Так как для образов загрузки можно использовать одно и то же имя образа в разных архитектурах, следует указать архитектуру для обеспечения правильного использования образа. |
| [/Филенаме: `<Filename>` ] | Указывает имя файла. Если образ не может быть однозначно определен по имени, необходимо указать имя файла. |
| FilterType`<Filtertype>` | Указывает атрибут пакета драйверов для поиска. В одной команде можно указать несколько атрибутов. Кроме того, необходимо указать **/оператор** и **/value** с этим параметром. Допустимые значения:<ul><li>PackageId</li><li>PackageName</li><li>паккажеенаблед</li><li>паккажедатеаддед</li><li>паккажеинффиленаме</li><li>паккажекласс<p>PackageProvider</li><li>паккажеарчитектуре</li><li>паккажелокале</li><li>паккажесигнед</li><li>паккажедатепублишед</li><li>Packageversion</li><li>дривердескриптион</li><li>дривермануфактурер</li><li>дриверхардвареид</li><li>дриверкомпатиблеид</li><li>дриверексклудеид</li><li>дриверграупид</li><li>Дриверграупнаме * *</li></ul>. |
| Станции`{Equal|NotEqual|GreaterOrEqual|LessOrEqual|Contains}` | Задает связь между атрибутом и значениями. Параметр **Contains** можно указывать только со строковыми атрибутами. Можно указать только **греатерорекуал** и **лессорекуал** с атрибутами даты и версии. |
| Значений`<Value>` | Указывает значение для поиска относительно указанного `<attribute>` . Можно указать несколько значений для одного **/филтертипе**. Для каждого фильтра доступны следующие значения:<ul><li>**PackageId** — укажите допустимый идентификатор GUID. Например: {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**PackageName** — укажите любое строковое значение.</li><li>**Паккажеенаблед** — укажите **Yes** или **No**</li><li>**Паккажедатеаддед** — укажите дату в следующем формате: гггг/мм/дд.</li><li>**Паккажеинффиленаме** — укажите любое строковое значение.</li><li>**Паккажекласс** — укажите допустимое имя класса или GUID класса. Например: **дискдриве**, **net**или {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**PackageProvider** — укажите любое строковое значение.</li><li>**Паккажеарчитектуре** — укажите **x86**, **x64**или **ia64**</li><li>**Паккажелокале** — укажите допустимый идентификатор языка. Например: **en-US** или **es-ES**</li><li>**Паккажесигнед** — укажите **Yes** или **No**</li><li>**Паккажедатепублишед** — укажите дату в следующем формате: гггг/мм/дд.</li><li>**Packageversion** — укажите версию в следующем формате: а.б.КС.и.. Например: 6.1.0.0</li><li>**Дривердескриптион** — укажите любое строковое значение.</li><li>**Дривермануфактурер** — укажите любое строковое значение.</li><li>**Дриверхардвареид** — укажите любое строковое значение.</li><li>**Дриверкомпатиблеид** — укажите любое строковое значение.</li><li>**Дриверексклудеид** — укажите любое строковое значение.</li><li>**Дриверграупид** — укажите допустимый идентификатор GUID. Например: {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**Дриверграупнаме** — укажите любое строковое значение.</li></ul> Дополнительные сведения об этих значениях см. в разделе [атрибуты драйвера и пакета](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759262(v=ws.11)). |

## <a name="examples"></a>Примеры

Чтобы добавить пакеты драйверов в загрузочный образ, введите одну из следующих ссылок:

```
wdsutil /add-ImageDriverPackagemedia:WinPE Boot Imagemediatype:Boot /Architecture:x86 /Filtertype:DriverGroupName /Operator:Equal /Value:x86Bus /Filtertype:PackageProvider /Operator:Contains /Value:Provider1 /Filtertype:Packageversion /Operator:GreaterOrEqual /Value:6.1.0.0
```

```
wdsutil /verbose /add-ImageDriverPackagemedia: WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filtertype:PackageClass /Operator:Equal /Value:Net /Filtertype:DriverManufacturer /Operator:NotEqual /Value:Name1 /Value:Name2 /Filtertype:Packagedateadded /Operator:LessOrEqual /Value:2008/01/01
```

```
wdsutil /verbose /add-ImageDriverPackagemedia:WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filtertype:PackageClass /Operator:Equal /Value:Net /Value:System /Value:DiskDrive /Value:HDC /Value:SCSIAdapter
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
-
- [Команда WDSUTIL Add-имажедриверпаккаже](wdsutil-add-imagedriverpackage.md)
-
- [Команда WDSUTIL Add-аллдриверпаккажес](wdsutil-add-alldriverpackages.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
