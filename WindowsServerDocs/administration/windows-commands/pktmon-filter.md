---
title: фильтр пктмон
description: Справочная статья по команде пктмон Filter.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: 80f3978105b0c73602c8ab04d78c48d80c88c444
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241213"
---
# <a name="pktmon-filter"></a>фильтр пктмон

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows 10, Azure Stack ХЦИ, центр Azure Stack, Azure

Фильтр пктмон позволяет выводить список, добавлять или удалять фильтры пакетов.

## <a name="syntax"></a>Синтаксис

```
pktmon filter { list | add | remove } [OPTIONS | help]
```

### <a name="parameters"></a>Параметры

| **Параметр** | **Описание** |
| ------------- | --------------- |
| **список фильтров пктмон** | Отображение активных фильтров пакетов. |
| **Добавление фильтра пктмон** |  Добавьте фильтр для управления переданными пакетами. |
| **Удаление фильтра пктмон** | Удалите все фильтры пакетов. |

## <a name="additional-references"></a>Дополнительные ссылки

- [пктмон](pktmon.md)
- [Пктмонная Comp](pktmon-comp.md)
- [Счетчики пктмон](pktmon-counters.md)
- [Добавление фильтра пктмон](pktmon-filter-add.md)
- [Формат пктмон](pktmon-format.md)
- [Список пктмон](pktmon-list.md)
- [Пктмон пкапнг](pktmon-pcapng.md)
- [Сброс пктмон](pktmon-reset.md)
- [Запуск пктмон](pktmon-start.md)
- [Выгрузка пктмон](pktmon-unload.md)
- [Общие сведения о мониторе пакетов](/windows-server/networking/technologies/pktmon/pktmon)
