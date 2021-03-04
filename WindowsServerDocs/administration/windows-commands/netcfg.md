---
title: netcfg
description: Справочная статья по команде netcfg, которая устанавливает среда предустановки Windows (WinPE), облегченную версию Windows, используемую для развертывания рабочих станций.
ms.topic: reference
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ed9acff1faa357a64c5f7c98221e7e721849be0b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101811162"
---
# <a name="netcfg"></a>netcfg

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Устанавливает среда предустановки Windows (WinPE), облегченную версию Windows, используемую для развертывания рабочих станций.

## <a name="syntax"></a>Синтаксис

```
netcfg [/v] [/e] [/winpe] [/l ] /c /i
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| /v | Выполняется в подробном (подробном) режиме. |
| /e | Использует переменные среды обслуживания во время установки и удаления. |
| /винпе | Устанавливает протоколы TCP/IP, NetBIOS и Microsoft Client для среды предустановки Windows (WinPE). |
| /l | Задает расположение INF-файла. |
| /C | Предоставляет класс устанавливаемого компонента. **протокол**, **Служба** или **клиент**. |
| /i | Предоставляет идентификатор компонента. |
| /s | Предоставляет тип отображаемых компонентов, включая **\та** для адаптеров или **n** для сетевых компонентов. |
| /b | Отображает пути привязки, за которым следует строка, содержащая имя пути. |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

Чтобы установить *Пример* протокола с помощью к:\оемдир\ексампле.инф, введите:

```
netcfg /l c:\oemdir\example.inf /c p /i example
```

Чтобы установить службу *MS_Server* , введите:

```
netcfg /c s /i MS_Server
```

Чтобы установить среду предустановки TCP/IP, NetBIOS и Microsoft Client для Windows, введите:

```
netcfg /v /winpe
```

Чтобы отобразить, если компонент *MS_IPX* установлен, введите:

```
netcfg /q MS_IPX
```

Чтобы удалить *MS_IPX* компонента, введите:

```
netcfg /u MS_IPX
```

Чтобы отобразить все установленные сетевые компоненты, введите:

```
netcfg /s n
```

Чтобы отобразить пути привязки, содержащие *MS_TCPIP*, введите:

```
netcfg /b ms_tcpip
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
