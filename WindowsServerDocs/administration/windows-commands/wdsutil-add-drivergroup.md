---
title: WDSUTIL Add-дриверграуп
description: Справочная статья по команде WDSUTIL Add-дриверграуп, которая добавляет группу драйверов на сервер.
ms.topic: reference
ms.assetid: 2a92fe8f-03f9-462a-b99e-f23275259807
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 68583ba35c141df03cbc5e351da6c4dc8ea4e161
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524619"
---
# <a name="wdsutil-add-drivergroup"></a>WDSUTIL Add-дриверграуп

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет группу драйверов на сервер.

## <a name="syntax"></a>Синтаксис

```
wdsutil /add-DriverGroup /DriverGroup:<Groupname>\n\ [/Server:<Servername>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}] [/Filtertype:<Filtertype> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /Дриверграуп:`<Groupname>` | Указывает имя новой группы драйверов. |
| Сервером`<Servername>` | Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
| Доступной`{Yes|No}` | Включает или отключает пакет. |
| Квартал`{Matched|All}` | Указывает, какие пакеты следует установить при соблюдении условий фильтра. **Сопоставление** означает установку только пакетов драйверов, соответствующих оборудованию клиента. **Все** означает установку всех пакетов на клиентах независимо от их оборудования. |
| FilterType`<Filtertype>` | Указывает тип фильтра, добавляемого в группу. В одной команде можно указать несколько типов фильтров. После каждого типа фильтра должен следовать **/полици** и хотя бы один **/value**. Допустимые значения:<ul><li>биосвендор</li><li>биосверсион</li><li>чассистипе</li><li>Изготовитель</li><li>Uuid</li><li>OSVersion</li><li>оседитион</li><li>ослангуаже</li></ul> Дополнительные сведения о получении значений для всех других типов фильтров см. в разделе [фильтры группы драйверов](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759191(v=ws.11)). |
| [/Полици: `{Include|Exclude}` ] | Задает политику, которая должна быть задана для фильтра. Если для **/полици** задано значение **включить**, то клиентские компьютеры, соответствующие фильтру, могут устанавливать драйверы в этой группе. Если **/полици** имеет значение **исключить**, то клиентские компьютеры, соответствующие фильтру, не смогут устанавливать драйверы в этой группе. |
| [/Value: `<Value>` ] | Указывает значение клиента, соответствующее **/филтертипе**. Можно указать несколько значений для одного типа. Сведения о допустимых значениях типа фильтра см. в разделе [фильтры группы драйверов](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759191(v=ws.11)). |

## <a name="examples"></a>Примеры

Чтобы добавить группу драйверов, введите:

```
wdsutil /add-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```

```
wdsutil /add-DriverGroup /DriverGroup:printerdrivers /Applicability:All /Filtertype:Manufacturer /Policy:Include /Value:Name1 /Filtertype:Chassistype /Policy:Exclude /Value:Tower /Value:MiniTower
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Add-дриверграуппаккаже](wdsutil-add-drivergrouppackage.md)

- [Команда WDSUTIL Add-дриверграуппаккажес](wdsutil-add-drivergrouppackages.md)

- [Команда WDSUTIL Add-дриверграупфилтер](wdsutil-add-drivergroupfilter.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
