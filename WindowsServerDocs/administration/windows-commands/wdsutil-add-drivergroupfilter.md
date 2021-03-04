---
title: Add-Дриверграупфилтер
description: Справочная статья по команде Add-Дриверграупфилтер, которая добавляет фильтр в группу драйверов на сервере.
ms.topic: reference
ms.assetid: a66c5e68-99ea-4e47-b68d-8109633ae336
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0402db6c153fd6a9ee6979c3641ef2ca76dbf5b5
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804207"
---
# <a name="add-drivergroupfilter"></a>Add-Дриверграупфилтер

Добавляет фильтр в группу драйверов на сервере.

## <a name="syntax"></a>Синтаксис

```
wdsutil /Add-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /Дриверграуп:`<Groupname>` | Указывает имя новой группы драйверов. |
| Сервером`<Servername>` | Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
| FilterType`<Filtertype>` | Указывает тип фильтра, добавляемого в группу. В одной команде можно указать несколько типов фильтров. После каждого типа фильтра должен следовать **/полици** и хотя бы один **/value**. Допустимые значения:<ul><li>биосвендор</li><li>биосверсион</li><li>чассистипе</li><li>Изготовитель</li><li>Uuid</li><li>OSVersion</li><li>оседитион</li><li>ослангуаже</li></ul> Дополнительные сведения о получении значений для всех других типов фильтров см. в разделе [фильтры группы драйверов](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759191(v=ws.11)). |
| [/Полици: `{Include|Exclude}` ] | Задает политику, которая должна быть задана для фильтра. Если для **/полици** задано значение **включить**, то клиентские компьютеры, соответствующие фильтру, могут устанавливать драйверы в этой группе. Если **/полици** имеет значение **исключить**, то клиентские компьютеры, соответствующие фильтру, не смогут устанавливать драйверы в этой группе. |
| [/Value: `<Value>` ] | Указывает значение клиента, соответствующее **/филтертипе**. Можно указать несколько значений для одного типа. Сведения о допустимых значениях типа фильтра см. в разделе [фильтры группы драйверов](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759191(v=ws.11)). |

## <a name="examples"></a>Примеры

Чтобы добавить фильтр в группу драйверов, введите:

```
wdsutil /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /Value:Name2
```

```
wdsutil /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /FilterType:ChassisType /Policy:Exclude /Value:Tower /Value:MiniTower
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Add-дриверграуппаккаже](wdsutil-add-drivergrouppackage.md)

- [Команда WDSUTIL Add-дриверграуппаккажес](wdsutil-add-drivergrouppackages.md)

- [Команда WDSUTIL Add-дриверграуп](wdsutil-add-drivergroup.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
