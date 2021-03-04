---
title: Remove-Дриверграупфилтер
description: Справочная статья по Remove-Дриверграупфилтер, которая удаляет правило фильтрации из группы драйверов на сервере.
ms.topic: reference
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a3c78219fb8f1aecf8d7a7bf4216f24e3e4ed87d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825571"
---
# <a name="remove-drivergroupfilter"></a>Remove-Дриверграупфилтер



Удаляет правило фильтрации из группы драйверов на сервере.

## <a name="syntax"></a>Синтаксис

```
wdsutil /Remove-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type>
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|/Дриверграуп:\<Group Name>|Указывает имя группы драйверов.|
|[/Server: \<Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.|
|[/Филтертипе: \<FilterType> ]|Указывает тип фильтра, удаляемого из группы. \<FilterType> может быть одним из следующих:</br>**биосвендор**</br>**биосверсион**</br>**ChassisType**</br>**Производителя**</br>**UUID**</br>**OsVersion**</br>**оседитион**</br>**ослангуаже**|

## <a name="examples"></a>Примеры

Чтобы удалить фильтр, введите один из следующих элементов:
```
wdsutil /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
wdsutil /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)