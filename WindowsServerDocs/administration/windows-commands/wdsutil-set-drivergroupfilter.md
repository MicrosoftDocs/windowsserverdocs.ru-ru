---
title: Набор подкоманд-Дриверграупфилтер
description: Справочная статья по подкоманде Set-Дриверграупфилтер, которая добавляет или удаляет существующий фильтр группы драйверов из группы драйверов.
ms.topic: reference
ms.assetid: 829ab1f0-4514-421e-9cc0-767b238da69c
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 059f834f66b342b064dd9e573f9a418419123897
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825128"
---
# <a name="subcommand-set-drivergroupfilter"></a>Подкоманда: Set-Дриверграупфилтер

Добавляет или удаляет существующий фильтр группы драйверов из группы драйверов.

## <a name="syntax"></a>Синтаксис

```
wdsutil /Set-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> [/Policy:{Include | Exclude}] [/AddValue:<Value> [/AddValue:<Value> ...]] [/RemoveValue:<Value> [/RemoveValue:<Value> ...]]
```

### <a name="parameters"></a>Параметры

|         Параметр          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                               Описание                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Дриверграуп:\<Group Name> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 Указывает имя группы драйверов.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|  [/Server: \<Server name> ]  |                                                                                                                                                                                                                                                                                                                                                                                                                Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| FilterType\<FilterType>  |                                                                                                                                                                                                                                                                       Указывает тип фильтра группы драйверов для добавления или удаления. В одной команде можно указать несколько фильтров. Для каждого **/филтертипе** можно добавить или удалить несколько значений с помощью **/ремовевалуе** и **/аддвалуе**. \<FilterType> может быть одним из следующих:</br>**биосвендор**</br>**биосверсион**</br>**ChassisType**</br>**Производителя**</br>**UUID**</br>**OsVersion**</br>**оседитион**</br>**ослангуаже**                                                                                                                                                                                                                                                                        |
|     [/Полици: {include      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                Exclude}]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|    [/Аддвалуе: \<Value> ]    | Указывает новое значение клиента, добавляемое в фильтр. Для одного типа фильтра можно указать несколько значений. Допустимые значения атрибутов для **чассистипе** см. в следующем списке. Сведения о получении значений для всех других типов фильтров см. в разделе [фильтры группы драйверов](https://go.microsoft.com/fwlink/?LinkID=155158) ( <https://go.microsoft.com/fwlink/?LinkID=155158> ).</br>**Другое**</br>**ункновнчассис**</br>**Рабочий стол**</br>**ловпрофиледесктоп**</br>**пиззабокс**</br>**минитовер**</br>**Вертикаль**</br>**Портативные**</br>**Ноутбук**</br>**Записная книжка**</br>**Перенос**</br>**доккингстатион**</br>**AllInOne**</br>**Подзаписная книжка**</br>**спацесавинг**</br>**лунчбокс**</br>**маинсистемчассис**</br>**експансиончассис**</br>**Подшасси**</br>**бусекспансиончассис**</br>**перифералчассис**</br>**сторажечассис**</br>**раккмаунтчассис**</br>**сеаледкасекомпутер**</br>**мултисистемчассис**</br>**компактпЦи**</br>**адванцедтка** |
|  [/Ремовевалуе: \<Value> ]   |                                                                                                                                                                                                                                                                                                                                                                                                                                     Указывает существующее значение клиента, которое необходимо удалить из фильтра, как указано в **/аддвалуе**.                                                                                                                                                                                                                                                                                                                                                                                                                                      |

## <a name="examples"></a>Примеры

Чтобы удалить фильтр, введите один из следующих элементов:
```
wdsutil /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /AddValue:Name1 /RemoveValue:Name2
```
```
wdsutil /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /RemoveValue:Name1 /FilterType:ChassisType /Policy:Exclude /AddValue:Tower /AddValue:MiniTower
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)