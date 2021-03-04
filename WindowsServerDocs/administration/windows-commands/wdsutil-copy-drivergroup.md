---
title: Copy-дриверграуп
description: Справочная статья по команде Copy-дриверграуп, которая дублирует существующую группу драйверов на сервере, включая фильтры, пакеты драйверов и состояние enabled/disabled.
ms.topic: reference
ms.assetid: 0aaf6fa5-8b5b-4a1e-ae9b-8b5c6d89f571
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: de02938c837409c9afa2f972d34cc67035c1175f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101803957"
---
# <a name="copy-drivergroup"></a>Copy-дриверграуп

Дублирует существующую группу драйверов на сервере, включая фильтры, пакеты драйверов, состояние включения или отключения.

## <a name="syntax"></a>Синтаксис

```
wdsutil /Copy-DriverGroup [/Server:<Server name>] /DriverGroup:<Source Groupname> /GroupName:<New Groupname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| Сервером`<Servername>` | Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
| /Дриверграуп:`<Source Groupname>` | Указывает имя исходной группы драйверов. |
| Группа`<New Groupname>` | Указывает имя новой группы драйверов. |

## <a name="examples"></a>Примеры

Чтобы скопировать группу драйверов, введите:

```
wdsutil /Copy-DriverGroup /Server:MyWdsServer /DriverGroup:PrinterDrivers /GroupName:X86PrinterDrivers
```

```
wdsutil /Copy-DriverGroup /DriverGroup:PrinterDrivers /GroupName:ColorPrinterDrivers
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
