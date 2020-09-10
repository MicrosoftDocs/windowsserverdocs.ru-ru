---
title: showmount
description: Справочная статья по шовмаунт, в которой отображаются подключенные каталоги.
ms.topic: reference
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e0a03c7e08c80e4cf0b99bbcb74aeff1deccdb1e
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640955"
---
# <a name="showmount"></a>showmount

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Для просмотра подключенных каталогов можно использовать **шовмаунт** .

## <a name="syntax"></a>Синтаксис
```
showmount {-e|-a|-d} <Server>
```

## <a name="description"></a>Описание
Программа командной строки **шовмаунт** \- отображает сведения о подключенных файловых системах, экспортированных сервером для NFS на компьютере, указанном *сервером*. Если *сервер* не указан, **шовмаунт** отображает сведения о компьютере, на котором выполняется команда **шовмаунт** .

Необходимо указать один из следующих параметров:

- ** \- e** — отображает все файловые системы, экспортированные на сервере.
- ** \- a** — отображает все NFS-клиенты сетевой файловой системы \( \) и каталоги на сервере, которые подключены.
- ** \- d** — отображает все каталоги на сервере, которые в настоящее время подключены клиентами NFS.

## <a name="see-also"></a>См. также:
[Справочник по командам служб для NFS](services-for-network-file-system-command-reference.md)