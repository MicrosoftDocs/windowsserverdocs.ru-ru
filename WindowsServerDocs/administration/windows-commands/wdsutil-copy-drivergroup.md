---
title: Copy-дриверграуп
description: Справочная статья по команде Copy-дриверграуп, которая дублирует существующую группу драйверов на сервере, включая фильтры, пакеты драйверов и состояние enabled/disabled.
ms.topic: reference
ms.assetid: 0aaf6fa5-8b5b-4a1e-ae9b-8b5c6d89f571
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 924f6181e424dad88a33f1421098e658275d1fa3
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524919"
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
