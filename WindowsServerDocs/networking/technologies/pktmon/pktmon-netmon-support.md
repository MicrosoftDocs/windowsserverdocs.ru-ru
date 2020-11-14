---
title: Поддержка пктмон для Microsoft Network Monitor (Netmon)
description: Эта страница используется для анализа созданных монитором пакетов ETL-файлов в Netmon.
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: 7c6e3a40558ea27a273464d157fa4fbdbacd7134
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632639"
---
# <a name="pktmon-support-for-microsoft-network-monitor-netmon"></a>Поддержка пктмон для Microsoft Network Monitor (Netmon)

>Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows 10, Azure Stack ХЦИ, центр Azure Stack, Azure

Монитор пакетов (Пктмон) создает журналы в формате ETL. Эти журналы можно анализировать с помощью Microsoft Network Monitor (Netmon) с помощью специальных средств синтаксического анализа. В этом разделе объясняется, как анализировать созданные монитором пакетов ETL-файлы в Netmon.

## <a name="network-monitor-setup-and-configuration"></a>Установка и Настройка сетевой монитор

Выполните следующие действия, чтобы установить и настроить Netmon для анализа файлов ETL, созданных монитором пакетов:

   1. [Установите сетевой монитор 3,4](/download/4865).
   1. Запуск сетевой монитор повышенными привилегиями и установка Windows в качестве активного профиля средства синтаксического анализа в (Сервис/параметры/профили средства синтаксического анализа).
   1. Скопируйте etl_Microsoft-Виндовс-пктмон-евентс. НПЛ [отсюда](https://github.com/microsoft/NetMon_Parsers_for_PacketMon/blob/main/etl_Microsoft-Windows-PktMon-Events.npl)   в%програмдата%\микрософт\нетворк Monitor 3 \ нпл\нетворкмонитор парсерс\виндовс.
   1. Скопируйте stub_etl_Microsoft-Виндовс-пктмон-евентс. НПЛ [отсюда](https://github.com/microsoft/NetMon_Parsers_for_PacketMon/blob/main/stub_etl_Microsoft-Windows-PktMon-Events.npl) в%програмдата%\микрософт\нетворк Monitor 3 \ нпл\нетворкмонитор парсерс\виндовс\стубс.
   1. Переименуйте stub_etl_Microsoft-Виндовс-пктмон-евентс. НПЛ в etl_Microsoft-Виндовс-пктмон-евентс. НПЛ
   1. Включите etl_Microsoft-Виндовс-пктмон-евентс. НПЛ в NetworkMonitor_Parsers_sparser. НПЛ в разделе "%Програмдата%\микрософт\нетворк Monitor 3 \ Нпл\нетворкмонитор parsers"
   1. Перезапустите сетевой монитор с повышенными правами для перестроения средств синтаксического анализа.

