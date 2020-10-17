---
title: WDSUTIL Add-дриверграуп
description: Справочная статья по WDSUTIL Add-дриверграуп, которая добавляет группу драйверов на сервер.
ms.topic: reference
ms.assetid: 2a92fe8f-03f9-462a-b99e-f23275259807
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 90c5f3427929d60f3c907746c88133606b239ded
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91731113"
---
# <a name="wdsutil-add-drivergroup"></a>WDSUTIL Add-дриверграуп

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет группу драйверов на сервер.

## <a name="syntax"></a>Синтаксис
```
wdsutil /add-DriverGroup /DriverGroup:<Group Name>\n\ [/Server:<Server name>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}] [/Filtertype:<Filter type> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]]
```
### <a name="parameters"></a>Параметры

|              Параметр              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     Описание                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      /Дриверграуп:<Group Name>      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     Указывает имя новой группы драйверов.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|        Сервером<Server name>        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|      /Enabled: {Yes &#124; No}       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           Включает или отключает пакет.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| /Аппликабилити: {сопоставлено &#124; все} |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        Указывает, какие пакеты следует установить при соблюдении условий фильтра. **Сопоставление** означает установку только пакетов драйверов, соответствующих оборудованию клиента. **Все** означает установку всех пакетов на клиентах независимо от их оборудования.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|      FilterType<Filtertype>       |                                                                                                                                                                                                                                                                          Указывает тип фильтра, добавляемого в группу. В одной команде можно указать несколько типов фильтров. После каждого типа фильтра должен следовать **/полици** и хотя бы один **/value**. <Filtertype> может быть одним из следующих:<p>**биосвендор**<p>**биосверсион**<p>**чассистипе**<p>**Производителя**<p>**UUID**<p>**OSVersion**<p>**оседитион**<p>**ослангуаже**<p>сведения о получении значений для всех других типов фильтров см. в разделе [фильтры группы драйверов](https://go.microsoft.com/fwlink/?LinkID=155158) ( <https://go.microsoft.com/fwlink/?LinkID=155158> ).                                                                                                                                                                                                                                                                           |
| [/Полици: {include &#124; Exclude}]  |                                                                                                                                                                                                                                                                                                                                                                                                                                                 Задает политику, которая должна быть задана для фильтра. Если для **/полици** задано значение **включить**, то клиентские компьютеры, соответствующие фильтру, могут устанавливать драйверы в этой группе. Если **/полици** имеет значение **исключить**, то клиентские компьютеры, соответствующие фильтру, не смогут устанавливать драйверы в этой группе.                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|          /Value<Value>]           | Указывает значение клиента, соответствующее **/филтертипе**. Можно указать несколько значений для одного типа. Допустимые значения для определенных типов фильтров см. в следующем списке. Следующие атрибуты предназначены для **чассистипе**. Сведения о получении значений для всех других типов фильтров см. в разделе [фильтры группы драйверов](https://go.microsoft.com/fwlink/?LinkID=155158) ( <https://go.microsoft.com/fwlink/?LinkID=155158> ).<p>**Другое**<p>**ункновнчассис**<p>**Рабочий стол**<p>**ловпрофиледесктоп**<p>**пиззабокс**<p>**минитовер**<p>**Вертикаль**<p>**Портативные**<p>**Ноутбук**<p>**Записная книжка**<p>**Перенос**<p>**доккингстатион**<p>**AllInOne**<p>**Подзаписная книжка**<p>**спацесавинг**<p>**лунчбокс**<p>**маинсистемчассис**<p>**експансиончассис**<p>**Подшасси**<p>**бусекспансиончассис**<p>**перифералчассис**<p>**стораечассис**<p>**раккмаунтчассис**<p>**сеаледкасекомпутер**<p>**мултисистемчассис**<p>**компактпЦи**<p>**адванцедтка** |

## <a name="examples"></a>Примеры
Чтобы добавить группу драйверов, введите одну из следующих:
```
wdsutil /add-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```
```
wdsutil /add-DriverGroup /DriverGroup:printerdrivers /Applicability:All /Filtertype:Manufacturer /Policy:Include /Value:Name1 /Filtertype:Chassistype /Policy:Exclude /Value:Tower /Value:MiniTower
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [вдсутиладд-дриверграуппаккаже, команда](wdsutil-add-drivergrouppackage.md)
- [вдсутиладд-дриверграуппаккажес, команда](wdsutil-add-drivergrouppackages.md)
- [вдсутиладд-дриверграупфилтер, команда](wdsutil-add-drivergroupfilter.md)