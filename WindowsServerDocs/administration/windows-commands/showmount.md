---
title: showmount
description: Справочная статья по команде шовмаунт, которая отображает сведения о подключенных файловых системах, экспортированных сервером для NFS на указанном компьютере.
ms.topic: reference
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3af87ba4ed42789cf07a2ae63ce9e720043a196e
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718331"
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