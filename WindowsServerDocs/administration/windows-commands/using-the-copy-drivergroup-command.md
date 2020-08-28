---
title: Copy-Дриверграуп
description: Справочная статья по Copy-Дриверграуп, которая дублирует существующую группу драйверов на сервере, включая фильтры, пакеты драйверов и состояние включения или отключения.
ms.topic: reference
ms.assetid: 0aaf6fa5-8b5b-4a1e-ae9b-8b5c6d89f571
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ccd6676ff0d925ee83eea5a4b159fc3e4bf72ba3
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038222"
---
# <a name="copy-drivergroup"></a>Copy-Дриверграуп

Дублирует существующую группу драйверов на сервере, включая фильтры, пакеты драйверов, состояние включения или отключения.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL /Copy-DriverGroup [/Server:<Server name>] /DriverGroup:<Source Group Name> /GroupName:<New Group Name>
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|[/Server: \<Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.|
|/Дриверграуп:\<Source Group Name>|Указывает имя исходной группы драйверов.|
|Группа\<New Group Name>|Указывает имя новой группы драйверов.|

## <a name="examples"></a>Примеры

Чтобы скопировать группу драйверов, введите одну из следующих:
```
WDSUTIL /Copy-DriverGroup /Server:MyWdsServer /DriverGroup:PrinterDrivers /GroupName:X86PrinterDrivers
```
```
WDSUTIL /Copy-DriverGroup /DriverGroup:PrinterDrivers /GroupName:ColorPrinterDrivers
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)