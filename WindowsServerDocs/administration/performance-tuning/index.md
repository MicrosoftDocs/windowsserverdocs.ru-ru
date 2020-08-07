---
title: Руководство по обеспечению высокой производительности Windows Server 2016
description: Руководство по обеспечению высокой производительности Windows Server 2016
ms.topic: landing-page
ms.author: phstee
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 69b65e9a7cb5e935a8c6b1a8ab500e33307a092d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896699"
---
# <a name="performance-tuning-guidelines-for-windows-server-2016"></a>Руководство по обеспечению высокой производительности Windows Server 2016

Если в организации выполняется серверная система, параметры сервера по умолчанию могут не соответствовать потребностям бизнеса. Например, может потребоваться наименьшее потребление электроэнергии, минимальная задержка или максимальная пропускная способность сервера. Это руководство содержит ряд рекомендаций, которые можно использовать для настройки параметров сервера в Windows Server 2016 и повышения производительности или экономии электроэнергии, особенно учитывая изменение характера рабочих нагрузки со временем.

Очень важно, чтобы при настройке учитывалось оборудование, рабочая нагрузка, бюджет питания и целевые показатели производительности сервера. В этом руководстве описывается каждый параметр и его возможное влияние. Это поможет вам принять обоснованное решение о его влиянии на систему, рабочую нагрузку, производительность и целевые показатели энергопотребления.

> [!warning]
> Параметры реестра и параметры настройки в разных версиях Windows Server существенно различаются. Обязательно применяйте последние рекомендации по настройке, чтобы избежать непредвиденных результатов.

## <a name="in-this-guide"></a>В данном руководстве
В этом руководстве рекомендации по обеспечению высокой производительности Windows Server 2016 разделены на три категории:

|настройка серверного оборудования; | Роль сервера | настройка подсистемы сервера. |
|:---:|:---:|:---:|
|[Рекомендации по обеспечению высокой производительности оборудования](hardware/index.md) |[Серверы Active Directory](role/active-directory-server/index.md) |[Управление памятью и кэшем](subsystem/cache-memory-management/index.md)|
|[Рекомендации по питанию оборудования](hardware/power.md)|[Файловые серверы](role/file-server/index.md)|[Подсистема сети](../../networking/technologies/network-subsystem/net-sub-performance-top.md)|
||[Серверы Hyper-V Server](role/hyper-v-server/index.md)|[Локальные дисковые пространства](subsystem/storage-spaces-direct/index.md)|
||[Службы удаленных рабочих столов](role/remote-desktop/session-hosts.md)|[Программно-конфигурируемая сеть (SDN)](subsystem/software-defined-networking/index.md)|
||[Веб-серверы](role/web-server/index.md)||
||[Контейнеры Windows Server](role/windows-server-container/index.md)||


## <a name="changes-in-this-version"></a>Изменения в этой версии

### <a name="sections-added"></a>Добавленные разделы
- [Рекомендации для конфигурации установки сервера Nano Server](../../get-started/getting-started-with-nano-server.md)


- [Программно-конфигурируемая сеть](subsystem/software-defined-networking/index.md), в том числе [HNV](subsystem/software-defined-networking/hnv-gateway-performance.md) и [инструкции по настройке шлюза SLB](subsystem/software-defined-networking/slb-gateway-performance.md).

- [Локальные дисковые пространства](subsystem/storage-spaces-direct/index.md)

- [HTTP 1.1 и HTTP 2](role/web-server/http-performance.md)

- [Контейнеры Windows Server](role/windows-server-container/index.md)

### <a name="sections-changed"></a>Измененные разделы

- Обновлено [руководство по Active Directory](role/active-directory-server/index.md).

- Обновлено [руководство по файловым серверам](role/file-server/index.md).

- Обновлено [руководство по веб-серверам](role/web-server/index.md).

- Обновлено [руководство по питанию оборудования](hardware/power.md).

- Обновлено [руководство по обеспечению высокой производительности PowerShell](powershell/index.md).

- Существенно обновлено [руководство по Hyper-V](role/hyper-v-server/index.md).

- *Удалено руководство по обеспечению высокой производительности рабочих нагрузок*, указатели на соответствующие ресурсы добавленные в [статью о дополнительных ресурсах по настройке](additional-resources.md).

- *Удалены разделы о выделенном хранилище* в пользу нового раздела [Локальные дисковые пространства](subsystem/storage-spaces-direct/index.md) и канонического содержимого TechNet.

- *Удален раздел о выделенных сетях* в пользу канонического содержимого TechNet.
