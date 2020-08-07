---
title: showmount
description: Справочная статья по шовмаунт, в которой отображаются подключенные каталоги.
ms.topic: article
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0be623eadd56a55a87f2df57fec9b4c6558770c9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882400"
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