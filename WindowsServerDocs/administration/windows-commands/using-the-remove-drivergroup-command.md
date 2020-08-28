---
title: Remove-Дриверграуп
description: Справочная статья по Remove-Дриверграуп, которая удаляет группу драйверов с сервера.
ms.topic: reference
ms.assetid: 1fefe9df-9782-433c-8abe-3f1a35e50da2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b2e0112ab1b85f37d148cb3f2b1c26b217b1047d
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038112"
---
# <a name="remove-drivergroup"></a>Remove-Дриверграуп

Удаляет группу драйверов с сервера.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL /Remove-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|/Дриверграуп:\<Group Name>|Указывает имя удаляемой группы драйверов.|
|[/Server: \<Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.|

## <a name="examples"></a>Примеры

Чтобы удалить группу драйверов, введите одну из следующих:
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers
```
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers /Server:MyWdsServer
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)