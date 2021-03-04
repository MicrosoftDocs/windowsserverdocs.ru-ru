---
title: Remove-Дриверграуп
description: Справочная статья по Remove-Дриверграуп, которая удаляет группу драйверов с сервера.
ms.topic: reference
ms.assetid: 1fefe9df-9782-433c-8abe-3f1a35e50da2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e13d521fa79f56a1b4e7aefb84d5bcc51b991ad7
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826513"
---
# <a name="remove-drivergroup"></a>Remove-Дриверграуп

Удаляет группу драйверов с сервера.

## <a name="syntax"></a>Синтаксис

```
wdsutil /Remove-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|/Дриверграуп:\<Group Name>|Указывает имя удаляемой группы драйверов.|
|[/Server: \<Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер.|

## <a name="examples"></a>Примеры

Чтобы удалить группу драйверов, введите одну из следующих:
```
wdsutil /Remove-DriverGroup /DriverGroup:PrinterDrivers
```
```
wdsutil /Remove-DriverGroup /DriverGroup:PrinterDrivers /Server:MyWdsServer
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)