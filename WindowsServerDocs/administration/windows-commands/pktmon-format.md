---
title: формат пктмон
description: Справочная статья по команде Format пктмон.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: f40ea62f4a15bc52a18a8e9bbccdc45745aaa93b
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241162"
---
# <a name="pktmon-format"></a>формат пктмон

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows 10, Azure Stack ХЦИ, центр Azure Stack, Azure

Формат пктмон преобразует файлы журнала в текстовый формат.

## <a name="syntax"></a>Синтаксис

```
pktmon format log.etl [-o log.txt] [-b] [-v [level]] [-x] [-e] [-l [port]
```

### <a name="parameters"></a>Параметры

| **Параметр** | **Описание** |
| ------------- | --------------- |
| **-o,--out** | Имя форматированного текстового файла. |
| **-s,--только статистика** | Отображает статистические сведения о файле журнала. |
| **-b,--Brief** | Сокращенный формат пакетов. |
| **-v, --verbose** | Уровень детализации [1.. 3]. |
| **-x,--Hex** | Шестнадцатеричный формат. |
| **-e,--No-Ethernet** | Не печатать заголовок Ethernet. |
| **-l,--вкслан** | Пользовательский порт ВКСЛАН. |

## <a name="additional-references"></a>Дополнительные ссылки

- [пктмон](pktmon.md)
- [Пктмонная Comp](pktmon-comp.md)
- [Счетчики пктмон](pktmon-counters.md)
- [Фильтр пктмон](pktmon-filter.md)
- [Добавление фильтра пктмон](pktmon-filter-add.md)
- [Список пктмон](pktmon-list.md)
- [Пктмон пкапнг](pktmon-pcapng.md)
- [Сброс пктмон](pktmon-reset.md)
- [Запуск пктмон](pktmon-start.md)
- [Выгрузка пктмон](pktmon-unload.md)
- [Общие сведения о мониторе пакетов](/windows-server/networking/technologies/pktmon/pktmon)
