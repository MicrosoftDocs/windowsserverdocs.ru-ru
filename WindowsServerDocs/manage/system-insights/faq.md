---
title: Вопросы и ответы по System Insights
description: Вопросы и ответы по System Insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 5/23/2018
ms.openlocfilehash: 2a97fdbc2e2a80c310cac2b770e18f34d53dd983
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997151"
---
# <a name="system-insights-faq"></a>Вопросы и ответы по System Insights

>Область применения: Windows Server 2019

## <a name="how-can-you-use-system-insights-with-azure-monitor-or-system-center-operations-manager"></a>Как можно использовать System Insights с Azure Monitor или System Center Operations Manager?

[Azure Monitor](https://azure.microsoft.com/services/monitor/) и [System Center Operations Manager](/system-center/scom/welcome?view=sc-om-1807) предоставлять операционную информацию по развертываниям, чтобы помочь вам управлять инфраструктурой. System Insights, напротив, — это компонент Windows Server, который предоставляет возможности локальной прогнозной аналитики. Система System Insights и Azure Monitor или SCOM позволяют распределять прогнозы по Генеральной совокупности устройств:

 Azure Monitor или SCOM могут выключать события, созданные системой System Insights, так как System Insights выводит результат каждого прогноза в журнал событий. Они могут отображать эти прогнозы для конкретного компьютера в пределах парка серверов Windows, что позволяет единообразно просматривать эти прогнозы в группе экземпляров сервера.

 Идентификаторы каналов и событий для каждого прогноза см. [здесь](./managing-capabilities.md#retrieving-capability-results).

## <a name="how-does-system-insights-relate-to-windows-ml"></a>Как система System Insights связана с Windows ML?

[Windows ML](/windows/uwp/machine-learning/) — это платформа, позволяющая разработчикам импортировать и оценить предварительно обученные модели машинного обучения на устройствах Windows. Эти модели получают преимущество от аппаратного ускорения, и их можно оценивать локально.

System Insights — это функция в Windows Server 2019, которая предоставляет локальные прогнозные возможности вместе с полноценным интерфейсом управления, включая PowerShell и интеграцию с центром администрирования Windows.

## <a name="can-i-use-system-insights-for-my-cluster"></a>Можно ли использовать System Insights для моего кластера?

Да. Система System Insights может независимо работать на каждом отдельном узле отказоустойчивого кластера и по умолчанию использование прогнозов System Insights в локальном хранилище, томе, ЦП и сети. **Можно также включить прогнозирование для кластерного хранилища**, чтобы возможности прогнозирования хранилища могли прогнозировать использование кластерных томов и хранилища.

Эти параметры можно управлять в центре администрирования Windows или PowerShell. более подробные сведения об этих функциях доступны [здесь](https://blogs.technet.microsoft.com/filecab/2018/10/03/using-system-insights-to-forecast-clustered-storage-usage/).


## <a name="how-expensive-is-it-to-run-the-default-capabilities"></a>Насколько дорогостоящей является запуск возможностей по умолчанию?

Каждая возможность по умолчанию недорога для запуска. Каждая возможность будет выполняться дольше, чем вы соберете дополнительные данные, но обычно они занимают всего несколько секунд.

## <a name="additional-references"></a>Дополнительные ссылки
Дополнительные сведения о System Insights см. в следующих ресурсах:

- [Обзор системной аналитики](overview.md)
- [Общие сведения о возможностях](understanding-capabilities.md)
- [Управление возможностями](managing-capabilities.md)
- [Добавление и разработка возможностей](adding-and-developing-capabilities.md)