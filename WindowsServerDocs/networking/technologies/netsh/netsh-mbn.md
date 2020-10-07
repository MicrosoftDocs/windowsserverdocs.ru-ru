---
title: Команды Netsh для мобильного широкополосного подключения
description: С помощью netsh mbn можно запрашивать и настраивать параметры мобильного широкополосного подключения.
ms.topic: article
author: apdutta
ms.author: apdutta
ms.date: 02/20/2020
ms.openlocfilehash: 926e28cff1815e5f6a82185ad78a3825ed188def
ms.sourcegitcommit: ad2c13b09044710bf14236308ade8d74877c3e0d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/30/2020
ms.locfileid: "91591164"
---
# <a name="netsh-mbn-commands"></a>Команды netsh mbn


С помощью **netsh mbn** можно запрашивать и настраивать параметры мобильного широкополосного подключения.

> [!TIP]
> Справку по команде netsh mbn можно получить с помощью команды
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;netsh mbn /?

Доступны следующие команды netsh mbn:

- [add](#add);
- [connect](#connect);
- [delete](#delete);
- [disconnect](#disconnect);
- [diagnose](#diagnose);
- [dump](#dump);
- [help](#help)
- [set](#set)
- [show](#show).
- [Тестирование](#test)

## <a name="add"></a>добавление

Позволяет добавить новый элемент конфигурации в таблицу.

Доступны следующие команды netsh mbn add:

- [dmprofile](#dmprofile);
- [profile](#profile).

### <a name="dmprofile"></a>dmprofile

Позволяет добавить профиль конфигурации мобильности данных в хранилище данных профиля.

**Синтаксис**

```powershell
add dmprofile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **name**      | Имя XML-файла профиля. Это имя XML-файла, содержащего данные профиля.     | Обязательный |


**Пример**

```powershell
add dmprofile interface="Cellular" name="Profile1.xml"
```


### <a name="profile"></a>профиль

Позволяет добавить профиль конфигурации сети в хранилище данных профиля.

**Синтаксис**

```powershell
add profile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **name**      | Имя XML-файла профиля. Это имя XML-файла, содержащего данные профиля.     | Обязательный |


**Пример**

```powershell
add profile interface="Cellular" name="Profile1.xml"
```


## <a name="connect"></a>подключение

Подключение к мобильной широкополосной сети

**Синтаксис**

```powershell
connect [interface=]<string> [connmode=]tmp|name [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **connmode**  | Указывает, как предоставляются параметры подключения. Для подключения можно указать XML-файл профиля или имя XML-файла профиля, ранее сохраненного в хранилище данных профилей мобильного широкополосного подключения с помощью команды "netsh mbn add profile". В первом случае параметр connmode должен содержать значение "tmp". Во втором случае ему присваивается значение "name".                                       | Обязательный |
| **name**      | Имя XML-файла профиля. Это имя XML-файла, содержащего данные профиля.     | Обязательный |


**Примеры**

```powershell
connect interface="Cellular" connmode=tmp name=d:\profile.xml
connect interface="Cellular" connmode=name name=MyProfileName
```


## <a name="delete"></a>"Удалить"

Позволяет удалить элемент конфигурации из таблицы.

Доступны следующие команды netsh mbn delete:

- [dmprofile](#dmprofile);
- [profile](#profile).

### <a name="dmprofile"></a>dmprofile

Позволяет удалить профиль конфигурации мобильности данных из хранилища данных профиля.

**Синтаксис**

```powershell
delete dmprofile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **name**      | Имя XML-файла профиля. Это имя XML-файла, содержащего данные профиля.     | Обязательный |

**Пример**

```powershell
delete dmprofile interface="Cellular" name="myProfileName"
```

### <a name="profile"></a>профиль

Удаляет профиль сети из хранилища данных профиля.

**Синтаксис**

```powershell
delete profile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **name**      | Имя XML-файла профиля. Это имя XML-файла, содержащего данные профиля.     | Обязательный |


**Пример**

```powershell
delete profile interface="Cellular" name="myProfileName"
```

## <a name="diagnose"></a>diagnose

Позволяет выполнить диагностику самых простых проблем сотовой сети.

**Синтаксис**

```powershell
diagnose [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
diagnose interface="Cellular"
```


## <a name="disconnect"></a>отключение

Отключается от мобильного широкополосного подключения.

**Синтаксис**

```powershell
disconnect [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
disconnect interface="Cellular"
```


## <a name="dump"></a>dump

Позволяет отобразить скрипт конфигурации.

Позволяет создать скрипт, который содержит текущую конфигурацию.  Сохранив этот скрипт в файл, с его помощью можно восстановить параметры конфигурации.

**Синтаксис**

```powershell
dump
```

## <a name="help"></a>справка

Позволяет вывести список команд.

**Синтаксис**

```powershell
help
```

## <a name="set"></a>set

Позволяет задать сведения о конфигурации.

Доступны следующие команды netsh mbn set:

- [acstate](#acstate);
- [dataenablement](#dataenablement);
- [dataroamcontrol](#dataroamcontrol);
- [enterpriseapnparams](#enterpriseapnparams);
- [highestconncategory](#highestconncategory);
- [powerstate](#powerstate);
- [profileparameter](#profileparameter);
- [slotmapping](#slotmapping);
- [tracing](#tracing).

### <a name="acstate"></a>acstate

Позволяет задать состояние автоматического мобильного широкополосного подключения для заданного интерфейса.

**Синтаксис**

```powershell
set acstate [interface=]<string> [state=]autooff|autoon|manualoff|manualon
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **name**      | Состояние автоматического подключения, которое нужно задать. Принимает одно из следующих значений:<br>autooff — маркер автоматического подключения отключен.<br>autoon — маркер автоматического подключения включен.<br>manualoff — Маркер подключения вручную отключен.<br>manualon — маркер подключения вручную включен. | Обязательный |


**Пример**

```powershell
set acstate interface="Cellular" state=autoon
```


### <a name="dataenablement"></a>dataenablement

Позволяет включить или отключить передачу данных по мобильному широкополосному подключению для заданного набора профилей и интерфейса.

**Синтаксис**

```powershell
set dataenablement [interface=]<string> [profileset=]internet|mms|all [mode=]yes|no
```

**Parameters**

|                |                                                                                               |          |
|----------------|-----------------------------------------------------------------------------------------------|----------|
| **interface**  | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **profileset** | Имя набора профиля.                                                                      | Обязательный |
| **mode**       | Принимает одно из следующих значений:<br>yes — включение целевого набора профиля.<br>no — отключение целевого набора профиля.| Обязательный |


**Пример**

```powershell
set dataenablement interface="Cellular" profileset=mms mode=yes
```


### <a name="dataroamcontrol"></a>dataroamcontrol

Позволяет задать состояние управления роумингом данных по мобильному широкополосному подключению для заданного набора профилей и интерфейса.

**Синтаксис**

```powershell
set dataroamcontrol [interface=]<string> [profileset=]internet|mms|all [state=]none|partner|all
```

**Parameters**

|                |                                                                                               |          |
|----------------|-----------------------------------------------------------------------------------------------|----------|
| **interface**  | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **profileset** | Имя набора профиля.                                                                      | Обязательный |
| **mode**       | Принимает одно из следующих значений:<br>none — только домашний оператор.<br>partner — домашний оператор и его партнеры.<br>all — домашний оператор, его партнеры и операторы роуминга.| Обязательный |


**Пример**

```powershell
set dataroamcontrol interface="Cellular" profileset=mms mode=partner
```


### <a name="enterpriseapnparams"></a>enterpriseapnparams

Позволяет задать параметры enterpriseAPN мобильного широкополосного подключения для заданного интерфейса.

**Синтаксис**

```powershell
set enterpriseapnparams [interface=]<string> [allowusercontrol=]yes|no|nc [allowuserview=]yes|no|nc [profileaction=]add|delete|modify|nc
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **allowusercontrol** | Принимает одно из следующих значений:<br>yes — разрешить пользователю управлять значением enterpriseAPN.<br>no — запретить пользователю управлять значением enterpriseAPN.<br>nc — без изменений. | Обязательный |
| **allowuserview** |Принимает одно из следующих значений:<br>yes — разрешить пользователю просматривать enterpriseAPN.<br>no — запретить пользователю просматривать enterpriseAPN.<br>nc — без изменений. | Обязательный |
| **profileaction** | Принимает одно из следующих значений:<br>add — профиль enterpriseAPN только что был добавлен.<br>delete — профиль enterpriseAPN только что был удален.<br>modify — профиль enterpriseAPN только что был изменен.<br>nc — без изменений. | Обязательный |


**Пример**

```powershell
set enterpriseapnparams interface="Cellular" profileset=mms mode=yes
```


### <a name="highestconncategory"></a>highestconncategory

Позволяет задать наивысшую категорию мобильного широкополосного подключения для указанного интерфейса.

**Синтаксис**

```powershell
set highestconncategory [interface=]<string> [highestcc=]admim|user|operator|device
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **highestcc** | Принимает одно из следующих значений:<br>admin — подготовленные администратором профили.<br>user — подготовленные пользователем профили.<br>operator — подготовленные оператором профили.<br>device — подготовленные устройством профили. | Обязательный |


**Пример**

```powershell
set highestconncategory interface="Cellular" highestcc=operator
```


### <a name="powerstate"></a>powerstate

Позволяет включить или отключить радиосвязь по мобильному широкополосному подключению для заданного интерфейса.

**Синтаксис**

```powershell
set powerstate [interface=]<string> [state=]on|off
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **state**      | Принимает одно из следующих значений:<br>on — питание приемопередатчика включено.<br>off — питание приемопередатчика отключено. | Обязательный |


**Пример**

```powershell
set powerstate interface="Cellular" state=on
```


### <a name="profileparameter"></a>profileparameter

Позволяет задать параметры в профиле мобильного широкополосного подключения.

**Синтаксис**

```powershell
set profileparameter [name=]<string> [[interface=]<string>] [[cost]=default|unrestricted|fixed|variable]
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | Имя изменяемого профиля. Если указан интерфейс, изменяется только профиль для этого интерфейса. | Обязательный |
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Необязательный |
| **cost**      | Стоимость, связанная с этим профилем.                                                             | Необязательный |


**Замечания**

Должен быть указан хотя бы один параметр между именем интерфейса и значением стоимости.


**Пример**

```powershell
set profileparameter name="profile 1" cost=default
```


### <a name="slotmapping"></a>slotmapping

Позволяет задать сопоставление слотов модема мобильного широкополосного подключения для указанного интерфейса.

**Синтаксис**

```powershell
set slotmapping [interface=]<string> [slotindex=]<integer>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **slotindex** | Индекс слота, который нужно установить.                                                                         | Обязательный |


**Пример**

```powershell
set slotmapping interface="Cellular" slotindex=1
```


### <a name="tracing"></a>tracing

Включение или отключение трассировки.

**Синтаксис**

```powershell
set tracing [mode=]yes|no
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **mode**      | Принимает одно из следующих значений:<br>yes: Позволяет включить трассировку для высокоскоростного мобильного подключения.<br>no — Позволяет отключить трассировку для высокоскоростного мобильного подключения.     | Обязательный |


**Пример**

```powershell
set tracing mode=yes
```

## <a name="show"></a>показать

Позволяет отобразить сведения о мобильном широкополосном подключении.

Доступны следующие команды netsh mbn show:

- [acstate](#acstate-1);
- [capability](#capability);
- [connection](#connection);
- [dataenablement](#dataenablement-1);
- [dataroamcontrol](#dataroamcontrol-1);
- [dmprofiles](#dmprofiles);
- [enterpriseapnparams](#enterpriseapnparams-1);
- [highestconncategory](#highestconncategory-1);
- [homeprovider](#homeprovider);
- [interfaces](#interfaces);
- [netlteattachinfo](#netlteattachinfo);
- [pin](#pin);
- [pinlist](#pinlist);
- [preferredproviders](#preferredproviders);
- [profiles](#profiles);
- [profilestate](#profilestate);
- [provisionedcontexts](#provisionedcontexts);
- [purpose](#purpose);
- [radio](#radio);
- [readyinfo](#readyinfo);
- [signal](#signal);
- [slotmapping](#slotmapping-1);
- [slotstatus](#slotstatus);
- [smsconfig](#smsconfig);
- [tracing](#tracing-1);
- [visibleproviders](#visibleproviders).

### <a name="acstate"></a>acstate

Позволяет отобразить сведения о состоянии автоматического подключения к мобильному широкополосному подключению для заданного интерфейса.

**Синтаксис**

```powershell
show acstate [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show acstate interface="Cellular"
```


### <a name="capability"></a>capability

Позволяет отобразить сведения о возможностях интерфейса для заданного интерфейса.

**Синтаксис**

```powershell
show capability [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show capability interface="Cellular"
```


### <a name="connection"></a>подключение

Позволяет отобразить сведения о текущем подключении для заданного интерфейса.

**Синтаксис**

```powershell
show connection [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show connection interface="Cellular"
```


### <a name="dataenablement"></a>dataenablement

Позволяет отобразить сведения о состоянии включения мобильного широкополосного подключения для заданного интерфейса.

**Синтаксис**

```powershell
show dataenablement [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show dataenablement interface="Cellular"
```


### <a name="dataroamcontrol"></a>dataroamcontrol

Позволяет отобразить сведения о состоянии управления роумингом мобильного широкополосного подключения для заданного интерфейса.

**Синтаксис**

```powershell
show dataroamcontrol [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show dataroamcontrol interface="Cellular"
```


### <a name="dmprofiles"></a>dmprofiles

Позволяет отобразить список профилей конфигурации мобильности данных, настроенных в системе.

**Синтаксис**

```powershell
show dmprofiles [[name=]<string>] [[interface=]<string>]
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | Имя отображаемого профиля.                                                               | Необязательный |
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Необязательный |

**Замечания**

Позволяет отобразить данные профиля или перечислить существующие в системе профили.

Если предоставлено имя профиля, отображается содержимое этого профиля. Если нет, перечисляются все профили для интерфейса.

Если предоставлено имя профиля, в списке будет указан только один профиль из заданного интерфейса. Если нет, отображается первый подходящий профиль.

**Пример**

```powershell
show dmprofiles name="profile 1" interface="Cellular"
show dmprofiles name="profile 2"
show dmprofiles
```


### <a name="enterpriseapnparams"></a>enterpriseapnparams

Позволяет отобразить параметры enterpriseAPN мобильного широкополосного подключения для заданного интерфейса.

**Синтаксис**

```powershell
show enterpriseapnparams [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show enterpriseapnparams interface="Cellular"
```


### <a name="highestconncategory"></a>highestconncategory

Позволяет отобразить наивысшую категорию мобильного широкополосного подключения для заданного интерфейса.

**Синтаксис**

```powershell
show highestconncategory [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show highestconncategory interface="Cellular"
```


### <a name="homeprovider"></a>homeprovider

Позволяет отобразить сведения о домашнем операторе для заданного интерфейса.

**Синтаксис**

```powershell
show homeprovider [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show homeprovider interface="Cellular"
```


### <a name="interfaces"></a>interfaces

Позволяет отобразить список присутствующих в системе интерфейсов мобильного широкополосного подключения. Параметры для этой команды не используются.

**Синтаксис**

```powershell
show interfaces
```


### <a name="netlteattachinfo"></a>netlteattachinfo

Позволяет отобразить параметры LTE attach мобильного широкополосного подключения для заданного интерфейса.

**Синтаксис**

```powershell
show netlteattachinfo [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show netlteattachinfo interface="Cellular"
```

### <a name="pin"></a>pin

Позволяет отобразить сведения о контактах для указанного интерфейса.

**Синтаксис**

```powershell
show pin [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show pin interface="Cellular"
```


### <a name="pinlist"></a>pinlist

Позволяет отобразить список контактов для указанного интерфейса.

**Синтаксис**

```powershell
show pinlist [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show pinlist interface="Cellular"
```


### <a name="preferredproviders"></a>preferredproviders

Позволяет отобразить список предпочтительных операторов для заданного интерфейса.

**Синтаксис**

```powershell
show preferredproviders [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show preferredproviders interface="Cellular"
```


### <a name="profiles"></a>profiles

Позволяет отобразить список профилей, настроенных в системе.

**Синтаксис**

```powershell
show profiles [[name=]<string>] [[interface=]<string>] [[purpose=]<string>]
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | Имя отображаемого профиля.                                                               | Необязательный |
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Необязательный |
| **purpose**   | Описание | Необязательный |

**Замечания**

Если предоставлено имя профиля, отображается содержимое этого профиля. Если нет, перечисляются все профили для интерфейса.

Если предоставлено имя профиля, в списке будет указан только один профиль из заданного интерфейса. Если нет, отображается первый подходящий профиль.

Если указана цель (purpose), отображаются только профили с соответствующим идентификатором цели.  Если нет, фильтрация профилей по цели не выполняется.  Эта строка может содержать GUID в фигурных скобках или одну из следующих строк: internet, supl, mms, ims или allhost.

**Пример**

```powershell
show profiles interface="Cellular" purpose="{00000000-0000-0000-0000-000000000000}"
show profiles name="profile 1" interface="Cellular"
show profiles name="profile 2"
show profiles
```

### <a name="profilestate"></a>profilestate

Позволяет отобразить сведения о состоянии профиля мобильного широкополосного подключения для заданного интерфейса.

**Синтаксис**

```powershell
show profilestate [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |
| **name**      | Имя профиля. Содержит имя профиля, для которого нужно отобразить сведения о состоянии.            | Обязательный |

**Пример**

```powershell
show profilestate interface="Cellular" name="myProfileName"
```

### <a name="provisionedcontexts"></a>provisionedcontexts

Позволяет отобразить сведения о подготовленных контекстах для заданного интерфейса.

**Синтаксис**

```powershell
show provisionedcontexts [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show provisionedcontexts interface="Cellular"
```


### <a name="purpose"></a>purpose

Позволяет отобразить идентификаторы групп целей, которые можно использовать для фильтрации профилей на устройстве. Параметры для этой команды не используются.

**Синтаксис**

```powershell
show purpose
```


### <a name="radio"></a>radio

Позволяет отобразить сведения о приемопередатчике для указанного интерфейса.

**Синтаксис**

```powershell
show radio [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show radio interface="Cellular"
```


### <a name="readyinfo"></a>readyinfo

Позволяет отобразить сведения о готовности для указанного интерфейса.

**Синтаксис**

```powershell
show readyinfo [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show readyinfo interface="Cellular"
```


### <a name="signal"></a>signal

Позволяет отобразить сведения о сигнале для указанного интерфейса.

**Синтаксис**

```powershell
show signal [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show signal interface="Cellular"
```


### <a name="slotmapping"></a>slotmapping

Позволяет отобразить сопоставление слотов модема мобильного широкополосного подключения для заданного интерфейса.

**Синтаксис**

```powershell
show slotmapping [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show slotmapping interface="Cellular"
```


### <a name="slotstatus"></a>slotstatus

Позволяет отобразить сведения о состоянии слота модема мобильного широкополосного подключения для заданного интерфейса.

**Синтаксис**

```powershell
show slotstatus [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show slotstatus interface="Cellular"
```


### <a name="smsconfig"></a>smsconfig

Позволяет отобразить сведения о конфигурации SMS для заданного интерфейса.

**Синтаксис**

```powershell
show smsconfig [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show smsconfig interface="Cellular"
```


### <a name="tracing"></a>tracing

Позволяет отобразить сведения о том, включена ли трассировка мобильного широкополосного подключения.

**Синтаксис**

```powershell
show tracing
```


### <a name="visibleproviders"></a>visibleproviders

Позволяет отобразить список видимых операторов для заданного интерфейса.

**Синтаксис**

```powershell
show visibleproviders [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Имя интерфейса. Одно из имен интерфейсов, которые отображаются с помощью команды "netsh mbn show interfaces". | Обязательный |


**Пример**

```powershell
show visibleproviders interface="Cellular"
```

## <a name="test"></a>Тестировать

Выполняет тесты для определенной функциональной области при сборе журналов.

**Синтаксис**
```
test [feature=<feature area>] [testPath=<path>] [taefPath=<path>] [param=<test input params>]
```

**Параметры**

| Tag | Значение | Является необязательным? |
|---|---|---|
| **feature** | Функциональная область за пределами поддерживаемых областей, перечисленных ниже. | Обязательно |
| **testpath** | Путь, содержащий двоичные файлы теста. | Необязательно, если установлен сервер HLK. |
| **taefpath** | Путь, содержащий двоичные файлы TAEF. | Необязательно, если установлен сервер HLK. |
| **param** | Параметры, разделенные запятыми, для использования в тестах. | Обязательно для некоторых функциональных областей, необязательно для других. |

**Замечания**

Поддерживаются следующие функциональные области:
- Подключение
- power
- radio
- esim
- sms
- dssa
- lte
- bringup

Для некоторых тестов требуются дополнительные параметры тестирования, которые необходимо указать в поле `param`.
Ниже перечислены обязательные параметры для функций.
- **connectivity**: AccessString, UserName (если применимо), Password (если применимо).
- **radio**: AccessString, UserName (если применимо), Password (если применимо).
- **esim**: ActivationCode
- **bringup**: AccessString, UserName (если применимо), Password (если применимо).

**Примеры**

```
test feature=connectivity param="AccessString=internet"
test feature=lte testpath="C:\\data\\test\\bin" taefpath="C:\\data\\test\\bin"
test feature=lte
```
