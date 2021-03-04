---
title: WDSUTIL Add-дриверграуппаккажес
description: Справочная статья по команде WDSUTIL Add-дриверграуппаккажес, которая добавляет пакеты группы драйверов.
ms.topic: reference
ms.assetid: 29022f53-ce14-4b2d-a81a-679c18e022b2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e9778e5f20bdeeb00d02d9ae7bb1caf23b1c68a7
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804157"
---
# <a name="wdsutil-add-drivergrouppackages"></a>WDSUTIL Add-дриверграуппаккажес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет пакеты группы драйверов.

## <a name="syntax"></a>Синтаксис

```
wdsutil /add-DriverGroupPackages /DriverGroup:<Group Name> [/Server:<Server Name>] /Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /Дриверграуп:`<Groupname>` | Указывает имя новой группы драйверов. |
| Сервером`<Servername>` | Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
| FilterType`<Filtertype>` | Указывает тип пакета драйверов для поиска. В одной команде можно указать несколько атрибутов. Кроме того, необходимо указать **/оператор** и **/value** с этим параметром. Допустимые значения:<ul><li>PackageId</li><li>PackageName</li><li>паккажеенаблед</li><li>паккажедатеаддед</li><li>паккажеинффиленаме</li><li>паккажекласс<p>PackageProvider</li><li>паккажеарчитектуре</li><li>паккажелокале</li><li>паккажесигнед</li><li>паккажедатепублишед</li><li>Packageversion</li><li>дривердескриптион</li><li>дривермануфактурер</li><li>дриверхардвареид</li><li>дриверкомпатиблеид</li><li>дриверексклудеид</li><li>дриверграупид</li><li>Дриверграупнаме * *</li></ul>. |
| Станции`{Equal|NotEqual|GreaterOrEqual|LessOrEqual|Contains}` | Задает связь между атрибутом и значениями. Параметр **Contains** можно указывать только со строковыми атрибутами. Можно указывать только значения **EQUAL**, **NotEqual**, **греатерорекуал** и **лессорекуал** с атрибутами даты и версии. |
| Значений`<Value>` | Указывает значение клиента, соответствующее **/филтертипе**. Можно указать несколько значений для одного **/филтертипе**. Для каждого фильтра доступны следующие значения:<ul><li>**PackageId** — укажите допустимый идентификатор GUID. Например: {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**PackageName** — укажите любое строковое значение.</li><li>**Паккажеенаблед** — укажите **Yes** или **No**</li><li>**Паккажедатеаддед** — укажите дату в следующем формате: гггг/мм/дд.</li><li>**Паккажеинффиленаме** — укажите любое строковое значение.</li><li>**Паккажекласс** — укажите допустимое имя класса или GUID класса. Например: **дискдриве**, **net** или {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**PackageProvider** — укажите любое строковое значение.</li><li>**Паккажеарчитектуре** — укажите **x86**, **x64** или **ia64**</li><li>**Паккажелокале** — укажите допустимый идентификатор языка. Например: **en-US** или **es-ES**</li><li>**Паккажесигнед** — укажите **Yes** или **No**</li><li>**Паккажедатепублишед** — укажите дату в следующем формате: гггг/мм/дд.</li><li>**Packageversion** — укажите версию в следующем формате: а.б.КС.и.. Например: 6.1.0.0</li><li>**Дривердескриптион** — укажите любое строковое значение.</li><li>**Дривермануфактурер** — укажите любое строковое значение.</li><li>**Дриверхардвареид** — укажите любое строковое значение.</li><li>**Дриверкомпатиблеид** — укажите любое строковое значение.</li><li>**Дриверексклудеид** — укажите любое строковое значение.</li><li>**Дриверграупид** — укажите допустимый идентификатор GUID. Например: {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**Дриверграупнаме** — укажите любое строковое значение.</li></ul> Дополнительные сведения об этих значениях см. в разделе [атрибуты драйвера и пакета](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759262(v=ws.11)). |

## <a name="examples"></a>Примеры

Чтобы добавить пакет группы драйверов, введите:

```
wdsutil /verbose /add-DriverGroupPackages /DriverGroup:printerdrivers /Filtertype:PackageClass /Operator:Equal /Value:printer /Filtertype:DriverManufacturer /Operator:NotEqual /Value:Name1 /Value:Name2
```

```
wdsutil /verbose /add-DriverGroupPackages /DriverGroup:DisplayDriversX86 /Filtertype:PackageClass /Operator:Equal /Value:Display /Filtertype:PackageArchitecture /Operator:Equal /Value:x86 /Filtertype:Packagedateadded /Operator:LessOrEqual /Value:2008/01/01
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Add-дриверпаккаже](wdsutil-add-driverpackage.md)

- [Команда WDSUTIL Add-дриверграуппаккаже](wdsutil-add-drivergrouppackage.md)

- [Команда WDSUTIL Add-аллдриверпаккажес](wdsutil-add-alldriverpackages.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
