---
title: выгрузка пктмон
description: Справочная статья по команде пктмон Unload.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: cc7313054445bdc72bd98cb60a7f4f6d11095553
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241194"
---
# <a name="pktmon-unload"></a>выгрузка пктмон

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows 10, Azure Stack ХЦИ, центр Azure Stack, Azure

Завершите работу службы драйвера Пктмон и выгрузите PktMon.sys. Фактически эквивалентно "sc.exe останавливаться Пктмон". Измерение (если активно) будет немедленно остановлено, и любое состояние будет удалено (счетчики, фильтры и т. д.).

## <a name="syntax"></a>Синтаксис

```
pktmon unload
```

## <a name="additional-references"></a>Дополнительные ссылки

- [пктмон](pktmon.md)
- [Пктмонная Comp](pktmon-comp.md)
- [Счетчики пктмон](pktmon-counters.md)
- [Фильтр пктмон](pktmon-filter.md)
- [Добавление фильтра пктмон](pktmon-filter-add.md)
- [Формат пктмон](pktmon-format.md)
- [Список пктмон](pktmon-list.md)
- [Пктмон пкапнг](pktmon-pcapng.md)
- [Сброс пктмон](pktmon-reset.md)
- [Запуск пктмон](pktmon-start.md)
- [Общие сведения о мониторе пакетов](/windows-server/networking/technologies/pktmon/pktmon)
