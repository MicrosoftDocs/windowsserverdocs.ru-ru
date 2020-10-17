---
title: Набор подкоманд-Дриверграупфилтер
description: Справочная статья по подкоманде Set-Дриверграупфилтер, которая добавляет или удаляет существующий фильтр группы драйверов из группы драйверов.
ms.topic: reference
ms.assetid: 829ab1f0-4514-421e-9cc0-767b238da69c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a27795fb6a4f6851a8b114f3ce1f91560df9ce76
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91731303"
---
# <a name="subcommand-set-drivergroupfilter"></a>Подкоманда: Set-Дриверграупфилтер

Добавляет или удаляет существующий фильтр группы драйверов из группы драйверов.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> [/Policy:{Include | Exclude}] [/AddValue:<Value> [/AddValue:<Value> ...]] [/RemoveValue:<Value> [/RemoveValue:<Value> ...]]
```

### <a name="parameters"></a>Параметры

|         Параметр          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                               Описание                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Дриверграуп:\<Group Name> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 Указывает имя группы драйверов.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|  [/Server: \<Server name> ]  |                                                                                                                                                                                                                                                                                                                                                                                                                Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| FilterType\<FilterType>  |                                                                                                                                                                                                                                                                       Указывает тип фильтра группы драйверов для добавления или удаления. В одной команде можно указать несколько фильтров. Для каждого **/филтертипе**можно добавить или удалить несколько значений с помощью **/ремовевалуе** и **/аддвалуе**. \<FilterType> может быть одним из следующих:</br>**биосвендор**</br>**биосверсион**</br>**ChassisType**</br>**Производителя**</br>**UUID**</br>**OsVersion**</br>**оседитион**</br>**ослангуаже**                                                                                                                                                                                                                                                                        |
|     [/Полици: {include      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                Exclude}]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|    [/Аддвалуе: \<Value> ]    | Указывает новое значение клиента, добавляемое в фильтр. Для одного типа фильтра можно указать несколько значений. Допустимые значения атрибутов для **чассистипе**см. в следующем списке. Сведения о получении значений для всех других типов фильтров см. в разделе [фильтры группы драйверов](https://go.microsoft.com/fwlink/?LinkID=155158) ( <https://go.microsoft.com/fwlink/?LinkID=155158> ).</br>**Другое**</br>**ункновнчассис**</br>**Рабочий стол**</br>**ловпрофиледесктоп**</br>**пиззабокс**</br>**минитовер**</br>**Вертикаль**</br>**Портативные**</br>**Ноутбук**</br>**Записная книжка**</br>**Перенос**</br>**доккингстатион**</br>**AllInOne**</br>**Подзаписная книжка**</br>**спацесавинг**</br>**лунчбокс**</br>**маинсистемчассис**</br>**експансиончассис**</br>**Подшасси**</br>**бусекспансиончассис**</br>**перифералчассис**</br>**сторажечассис**</br>**раккмаунтчассис**</br>**сеаледкасекомпутер**</br>**мултисистемчассис**</br>**компактпЦи**</br>**адванцедтка** |
|  [/Ремовевалуе: \<Value> ]   |                                                                                                                                                                                                                                                                                                                                                                                                                                     Указывает существующее значение клиента, которое необходимо удалить из фильтра, как указано в **/аддвалуе**.                                                                                                                                                                                                                                                                                                                                                                                                                                      |

## <a name="examples"></a>Примеры

Чтобы удалить фильтр, введите один из следующих элементов:
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /AddValue:Name1 /RemoveValue:Name2
```
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /RemoveValue:Name1 /FilterType:ChassisType /Policy:Exclude /AddValue:Tower /AddValue:MiniTower
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)