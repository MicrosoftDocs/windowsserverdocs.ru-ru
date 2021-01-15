---
title: пктмон пкапнг
description: Справочная статья по команде пктмон пкапнг.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: 7b906efd5548b6aa22168294668a1bde6da3c3c8
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241154"
---
# <a name="pktmon-pcapng"></a>пктмон пкапнг

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows 10, Azure Stack ХЦИ, центр Azure Stack, Azure

Пктмон пкапнг преобразует файлы журнала в формат пкапнг. Пропущенные пакеты не включаются по умолчанию.

## <a name="syntax"></a>Синтаксис

```
pktmon pcapng log.etl [-o log.pcapng]
```

### <a name="parameters"></a>Параметры

| **Параметр** | **Описание** |
| ------------- | --------------- |
| **-o,--out** | Имя форматированного файла пкапнг. |
| **-d,--только Drop** | Преобразовывать только пропущенные пакеты. |
| **-c,--Component-ID** | Фильтрация пакетов по определенному ИДЕНТИФИКАТОРу компонента. |

## <a name="example"></a>Пример

В следующем примере выполняется преобразование только отброшенных пакетов из сетевых карт в файле журнала *пктмон. ETL* в формат пкапнг:

```powershell
C:\Test> pktmon pcapng C:\tmp\PktMon.etl -d -c nics
```

## <a name="additional-references"></a>Дополнительные ссылки

- [пктмон](pktmon.md)
- [Пктмонная Comp](pktmon-comp.md)
- [Счетчики пктмон](pktmon-counters.md)
- [Фильтр пктмон](pktmon-filter.md)
- [Добавление фильтра пктмон](pktmon-filter-add.md)
- [Формат пктмон](pktmon-format.md)
- [Список пктмон](pktmon-list.md)
- [Выгрузка пктмон](pktmon-unload.md)
- [Сброс пктмон](pktmon-reset.md)
- [Запуск пктмон](pktmon-start.md)
- [Общие сведения о мониторе пакетов](/windows-server/networking/technologies/pktmon/pktmon)
