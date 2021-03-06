---
title: Предварительная оценка функций службы времени Windows в Windows Server 2019
description: Новые функции службы времени Windows в Windows Server 2019
author: dahavey
ms.author: dahavey
ms.date: 06/06/2020
ms.topic: article
ms.openlocfilehash: 01968fe51d25f394e346cebc8dbeafd2dd17ca4a
ms.sourcegitcommit: b5b040a47cf48c94852de9aad8b91475f891d2f7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2020
ms.locfileid: "88563374"
---
# <a name="insider-preview"></a>Предварительная оценка


## <a name="leap-second-support"></a>Поддержка корректировочной секунды

> Применяется к: Windows Server 2019 и Windows 10 версии 1809

Корректировочной секундой называется изменение времени UTC на 1 секунду, которая выполняется нерегулярно. Из-за постепенного замедления вращения Земли время [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (по атомным часам) немного отклоняется от [среднего солнечного времени](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time) (астрономического). Когда такое расхождение достигает 0,9 секунды, к времени UTC добавляется [корректировочная секунда](https://en.wikipedia.org/wiki/Leap_second), чтобы сохранить синхронизацию со средним солнечным временем.

Корректировочные секунды стали важны с учетом современных нормативных требований к точности и отслеживаемости в США и странах Европейского союза.

Дополнительная информация:

- Наш [блог с объявлениями](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- Руководство по проверке для [разработчиков](https://aka.ms/Dev-LeapSecond)

- Руководство по проверке для [ИТ-специалистов](https://aka.ms/ITPro-LeapSecond)


## <a name="precision-time-protocol"></a>Протокол точного времени

> Применяется к: Windows Server 2019 и Windows 10 версии 1809

Новый поставщик времени, входящий в Windows Server 2019 и Windows 10 (версия 1809), позволяет синхронизировать время с использованием PTP (протокол точного времени). Распространение информации о времени по сети сталкивается с сетевой задержкой. Если такая задержка не учитывается или не является симметричной, полученная от сервера отметка времени теряет смысл. Протокол PTP позволяет сетевым устройствам добавлять к измерениям времени задержку, вносимую каждым сетевым устройством, существенно повышая точность выборки времени для клиента Windows.

Дополнительная информация:

- Наш [блог с объявлениями](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- Руководство по проверке для [ИТ-специалистов](https://aka.ms/PTPValidation)


## <a name="software-timestamping"></a>Установка меток времени программным образом

> Применяется к: Windows Server 2019 и Windows 10 версии 1809

При получении по сети пакета времени от сервера он сначала обрабатывается сетевым стеком операционной системы, и лишь затем поступает в службу времени. Каждый компонент сетевого стека вносит некоторую задержку неизвестной величины, что снижает точность измерений времени.

![Установка меток времени программным образом](../media/Windows-Time-Service/software-timestamping.png)

Чтобы устранить эту проблему, используется программная установка меток времени в точках до и после обработки в сетевых компонентах Windows, как показано выше, что позволяет учесть задержку в операционной системе.

Дополнительная информация:

- Наш [блог с объявлениями](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- [Руководства по проверке для разработчиков и ИТ-специалистов](https://github.com/microsoft/W32Time/tree/master/Leap%20Seconds)


---
