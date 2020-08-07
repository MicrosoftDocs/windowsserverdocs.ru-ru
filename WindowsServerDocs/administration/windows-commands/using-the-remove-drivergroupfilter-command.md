---
title: Remove-Дриверграупфилтер
description: Справочная статья по Remove-Дриверграупфилтер, которая удаляет правило фильтрации из группы драйверов на сервере.
ms.topic: article
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 902dd41e7efbb8d7821737d4555a3e5ef957a17a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896368"
---
# <a name="remove-drivergroupfilter"></a>Remove-Дриверграупфилтер



Удаляет правило фильтрации из группы драйверов на сервере.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type>
```

### <a name="parameters"></a>Параметры

|Параметр|Описание:|
|---------|-----------|
|/Дриверграуп:\<Group Name>|Указывает имя группы драйверов.|
|[/Server: \<Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.|
|[/Филтертипе: \<FilterType> ]|Указывает тип фильтра, удаляемого из группы. \<FilterType>может быть одним из следующих:</br>**биосвендор**</br>**биосверсион**</br>**ChassisType**</br>**Производителя**</br>**UUID**</br>**OsVersion**</br>**оседитион**</br>**ослангуаже**|

## <a name="examples"></a>Примеры

Чтобы удалить фильтр, введите один из следующих элементов:
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)