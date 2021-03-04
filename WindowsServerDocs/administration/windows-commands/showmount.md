---
title: showmount
description: Справочная статья по команде шовмаунт, которая отображает сведения о подключенных файловых системах, экспортированных сервером для NFS на указанном компьютере.
ms.topic: reference
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b7032b23c0908c27e9f220050ab92a0e2f127351
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805707"
---
# <a name="showmount"></a>showmount

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Шовмаунт** можно использовать для вывода сведений о подключенных файловых системах, экспортированных сервером для NFS на указанном компьютере. Если сервер не указан, эта команда отображает сведения о компьютере, на котором выполняется команда **шовмаунт** .

## <a name="syntax"></a>Синтаксис

```
showmount {-e|-a|-d} <server>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| -E | Отображает все файловые системы, экспортированные на сервере. |
| -a | Отображает все клиенты сетевой файловой системы (NFS) и каталоги на сервере, которые подключены. |
| -d | Отображает все каталоги на сервере, которые в настоящее время подключены клиентами NFS. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Справочник по командам служб для NFS](services-for-network-file-system-command-reference.md)