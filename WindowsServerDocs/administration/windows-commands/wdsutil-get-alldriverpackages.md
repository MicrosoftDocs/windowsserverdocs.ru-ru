---
title: WDSUTIL Get-аллдриверпаккажес
description: Справочная статья по команде WDSUTIL Get-аллдриверпаккажес, которая отображает сведения обо всех пакетах драйверов на сервере, соответствующих указанным условиям поиска.
ms.topic: reference
ms.assetid: 9eb8fcb7-ef46-4c8d-9623-8969a3c8b8a4
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 64d64319a95e61953d6e3109ad367c101475b7b2
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825288"
---
# <a name="wdsutil-get-alldriverpackages"></a>WDSUTIL Get-аллдриверпаккажес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сведения обо всех пакетах драйверов на сервере, соответствующих указанным условиям поиска.

## <a name="syntax"></a>Синтаксис

```
wdsutil /get-alldriverpackages [/server:<servername>] [/show:{drivers | files | all}] [/filtertype:<filtertype> /operator:{equal | notequal | greaterorequal | lessorequal | contains} /value:<value> [/value:<value> ...]]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `[/server:<servername>] `| Имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
| `[/show:{drivers | files | all}]` | Указывает сведения о пакете для вывода. Если значение **/Show** не указано, по умолчанию возвращаются только метаданные пакета драйвера. **Драйверы** отображает список драйверов в пакете, **файлы** отображает список файлов в пакете, а **все** драйверы и файлы. |
| `/filtertype:<filtertype>` | Указывает атрибут пакета драйверов для поиска. В одной команде можно указать несколько атрибутов. Кроме того, необходимо указать **/оператор** и **/value** с этим параметром.<p>`<filtertype>`Может принимать одно из следующих действий:<ul><li>PackageId</li><li>PackageName</li><li>паккажеенаблед</li><li>паккажедатеаддед</li><li>паккажеинффиленаме</li><li>паккажекласс</li><li>PackageProvider</li><li>паккажеарчитектуре</li><li>паккажелокале</li><li>паккажесигнед</li><li>паккажедатепублишед</li><li>Packageversion</li><li>дривердескриптион</li><li>дривермануфактурер</li><li>дриверхардвареид</li><li>дриверкомпатиблеид</li><li>дриверграупид</li><li>дриверграупнаме</li></ul> |
| `/operator:{equal | notequal | greaterorequal | lessorequal | contains}` | Задает связь между атрибутом и значениями. Можно указать параметр **Contains** только со строковыми атрибутами. Можно указать **греатерорекуал** и **лессорекуал** только с атрибутами даты и версии. |
| `/value:<value>` | Задает значение для поиска заданного значения `<attribute>` . Можно указать несколько значений для одного **/филтертипе**. В списке ниже приведены атрибуты, которые можно указать для каждого фильтра. Дополнительные сведения об этих атрибутах см. в разделе [атрибуты драйвера и пакета](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759262(v=ws.11)). Атрибуты могут включать:<ul><li>**PackageId.** Указывает допустимый идентификатор GUID. Например: {4D36E972-E325-11CE-BFC1-08002BE10318}.</li><li>**PackageName.** Указывает любое строковое значение.</li><li>**Паккажеенаблед.** Указывает *Да* или *нет*.</li><li>**Паккажедатеаддед.** Указывает дату в следующем формате: гггг/мм/дд.</li><li>**Паккажеинффиленаме.** Указывает любое строковое значение.</li><li>**Паккажекласс.** Указывает допустимое имя класса или GUID класса. Например: *дискдриве*, *net* или *{4D36E972-E325-11CE-BFC1-08002BE10318}*.</li><li>**PackageProvider.** Указывает любое строковое значение.</li><li>**Паккажеарчитектуре.** Указывает *x86*, *x64* или *ia64*.</li><li>**Паккаглокале.** Указывает допустимый идентификатор языка. Например: *en-US* или *es-ES*.</li><li>**Паккажесигнед.** Указывает **Да** или **нет**.</li><li>**Паккажедатепублишед.** Указывает дату в следующем формате: гггг/мм/дд.</li><li>**Packageversion.** Указывает версию в следующем формате: а.б.КС.и.. Например: 6.1.0.0.</li><li>**Дривердескриптион.** Указывает любое строковое значение.</li><li>**Дривермануфактурер.** Указывает любое строковое значение.</li><li>**Дриверхардвареид.** Указывает любое строковое значение.</li><li>**Дриверкомпатиблеид.** Указывает любое строковое значение.</li><li>**Дриверексклудеид.** Указывает любое строковое значение.</li><li>**Дриверграупид.** Указывает допустимый идентификатор GUID. Например: {4D36E972-E325-11CE-BFC1-08002BE10318}.</li><li>**Дриверграупнаме.** Указывает любое строковое значение.</li></ul> |

## <a name="examples"></a>Примеры

Чтобы отобразить сведения, введите:

```
wdsutil /get-alldriverpackages /server:MyWdsServer /show:all /filtertype:drivergroupname /operator:contains /value:printer /filtertype:packagearchitecture /operator:equal /value:x64 /value:x86
```

```
wdsutil /get-alldriverpackages /show:drivers /filtertype:packagedateadded /operator:greaterorequal /value:2008/01/01
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Get-дриверпаккаже](wdsutil-get-driverpackage.md)

- [Команда WDSUTIL Get-дриверпаккажефиле](wdsutil-get-driverpackagefile.md)
