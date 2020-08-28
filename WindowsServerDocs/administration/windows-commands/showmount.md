---
title: showmount
description: Справочная статья по шовмаунт, в которой отображаются подключенные каталоги.
ms.topic: reference
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba118e711af040bba7dd6c1e63a14405b3116743
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024798"
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

## <a name="see-also"></a>См. также
[Справочник по командам служб для NFS](services-for-network-file-system-command-reference.md)