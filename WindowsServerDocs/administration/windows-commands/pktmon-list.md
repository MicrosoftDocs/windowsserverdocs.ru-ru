---
title: Список пктмон
description: Справочная статья по команде пктмон List.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: 6f03eccb554c1a63f4a798b9896709e6ba69be8c
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241210"
---
# <a name="pktmon-list"></a>Список пктмон

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows 10, Azure Stack ХЦИ, центр Azure Stack, Azure

Список всех активных компонентов, позволяющий изучить макет сетевого стека. Команда отображает сетевые компоненты (драйверы), упорядоченные по привязкам адаптеров.

## <a name="syntax"></a>Синтаксис

```
pktmon [comp] list
```

### <a name="parameters"></a>Параметры

| **Параметр** | **Описание** |
| ------------- | --------------- |
| **-i,--показывать-скрыто** | Отображение компонентов, скрытых по умолчанию. |
| **--JSON** | Вывод списка в формате JSON. |

## <a name="additional-references"></a>Дополнительные ссылки

- [пктмон](pktmon.md)
- [Пктмонная Comp](pktmon-comp.md)
- [Счетчики пктмон](pktmon-counters.md)
- [Фильтр пктмон](pktmon-filter.md)
- [Добавление фильтра пктмон](pktmon-filter-add.md)
- [Формат пктмон](pktmon-format.md)
- [Пктмон пкапнг](pktmon-pcapng.md)
- [Сброс пктмон](pktmon-reset.md)
- [Запуск пктмон](pktmon-start.md)
- [Выгрузка пктмон](pktmon-unload.md)
- [Общие сведения о мониторе пакетов](/windows-server/networking/technologies/pktmon/pktmon)
