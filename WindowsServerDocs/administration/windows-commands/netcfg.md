---
title: netcfg
description: Справочный раздел по команде netcfg, которая устанавливает среда предустановки Windows (WinPE), облегченную версию Windows, используемую для развертывания рабочих станций.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a308441df55873b205972d703ec52f53345beb5
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721557"
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
| /C | Предоставляет класс устанавливаемого компонента. **протокол**, **Служба**или **клиент**. |
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

Чтобы удалить *MS_IPX*компонента, введите:

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
