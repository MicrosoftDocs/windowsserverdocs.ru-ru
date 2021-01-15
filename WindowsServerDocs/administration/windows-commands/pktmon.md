---
title: пктмон
description: Справочная статья о средстве диагностики сети пктмон для Windows, которое можно использовать для записи пакетов, обнаружения пакетов, фильтрации пакетов и подсчета.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: 55b8ad90ca49349482e5e4b9ccb2ad11132a044d
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241157"
---
# <a name="pktmon"></a>пктмон

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows 10, Azure Stack ХЦИ, центр Azure Stack, Azure

Монитор пакетов (Пктмон) — это встроенное средство диагностики сети для Windows. Он может использоваться для записи пакетов, обнаружения, фильтрации и подсчета. Пктмон особенно полезен в сценариях виртуализации, таких как сети контейнеров и SDN, так как он обеспечивает видимость в сетевом стеке.

## <a name="syntax"></a>Синтаксис

```
pktmon { filter | comp | reset | counters | format | list | start | stop | pcapng | unload | help } [options]
```

### <a name="commands"></a>Команды

| **Команда** | **Описание** |
| --------- | ----------- |
| [фильтр пктмон](pktmon-filter.md) | Управление фильтрами пакетов. |
| [пктмонная Comp](pktmon-comp.md) | Управление зарегистрированными компонентами. |
| [Сброс пктмон](pktmon-reset.md) | Сбросить счетчики до нуля. |
| [Счетчики пктмон](pktmon-counters.md) | Счетчики пакетов запросов. |
| [формат пктмон](pktmon-format.md) | Преобразование файла журнала в текст. |
| [Список пктмон](pktmon-list.md) | Список всех активных компонентов. |
| [Запуск пктмон](pktmon-start.md) | Запуск мониторинга пакетов. |
| пктмон | Останавливает мониторинг пакетов. |
| [пктмон пкапнг](pktmon-pcapng.md) | Преобразование файла журнала в формат пкапнг. |
| [выгрузка пктмон](pktmon-unload.md) | Выгрузить драйвер пктмон. |
| Справка пктмон | Отображает краткую сводку по подкомандам. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Общие сведения о мониторе пакетов](/windows-server/networking/technologies/pktmon/pktmon)
- [Поддержка пктмон для Microsoft Network Monitor (Netmon)](/windows-server/networking/technologies/pktmon/pktmon-netmon-support)
