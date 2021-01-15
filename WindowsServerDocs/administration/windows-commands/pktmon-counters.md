---
title: Счетчики пктмон
description: Справочная статья по команде счетчиков пктмон.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: df61499d96ec8b9eee6ee2939860e95431478b52
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241223"
---
# <a name="pktmon-counters"></a>Счетчики пктмон

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows 10, Azure Stack ХЦИ, центр Azure Stack, Azure

Счетчики пктмон позволяют запрашивать и отображать текущие счетчики для каждого компонента, чтобы убедиться в наличии ожидаемого трафика и получить общее представление о том, как проходит трафик на компьютере.

## <a name="syntax"></a>Синтаксис

```
pktmon [comp] counters [-t { all | drop | flow }] [-z] [--json]
```

### <a name="parameters"></a>Параметры

| **Параметр** | **Описание** |
| ------------- | --------------- |
| **-t,--Counter-Type** | Выберите типы отображаемых счетчиков. Поддерживаемые значения: все счетчики (по умолчанию), только удаление или только потоки. |
| **-z,--Показывать-нули** | Показывать нулевые счетчики в обоих направлениях. |
| **-i,--показывать-скрыто** | Отображение компонентов, скрытых по умолчанию. |
| **--JSON** | Вывод счетчиков в формате JSON. |

## <a name="additional-references"></a>Дополнительные ссылки

- [пктмон](pktmon.md)
- [Пктмонная Comp](pktmon-comp.md)
- [Фильтр пктмон](pktmon-filter.md)
- [Добавление фильтра пктмон](pktmon-filter-add.md)
- [Формат пктмон](pktmon-format.md)
- [Список пктмон](pktmon-list.md)
- [Пктмон пкапнг](pktmon-pcapng.md)
- [Сброс пктмон](pktmon-reset.md)
- [Запуск пктмон](pktmon-start.md)
- [Выгрузка пктмон](pktmon-unload.md)
- [Общие сведения о мониторе пакетов](/windows-server/networking/technologies/pktmon/pktmon)
