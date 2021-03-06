---
title: Добавление и разработка возможностей
description: System Insights позволяет добавлять новые прогнозные возможности в System Insights, не требуя обновления операционной системы. Это позволяет разработчикам, в том числе корпорации Майкрософт и третьим лицам, создавать и предоставлять новые возможности в середине выпуска для решения наиболее важных сценариев. Новые возможности могут указывать пользовательские данные для собираются и анализа, а также интегрируются с существующими плоскостями управления System Insights.
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: d85016fd3f338ab87d6516815ee04c652875bdf5
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766767"
---
# <a name="adding-and-developing-new-capabilities"></a>Добавление и разработка новых возможностей

>Область применения: Windows Server 2019

System Insights позволяет добавлять новые прогнозные возможности в System Insights, не требуя обновления операционной системы. Это позволяет разработчикам, в том числе корпорации Майкрософт и третьим лицам, создавать и предоставлять новые возможности в середине выпуска для решения наиболее важных сценариев.

Любая новая возможность может интегрироваться с существующей инфраструктурой System Insights и расширяться на нее:

- Новые возможности могут **указывать любой счетчик производительности или системное событие**, которое будет собираться, сохраняться локально и возвращаться к возможности для анализа при вызове этой возможности.
- Новые возможности могут **использовать существующий центр администрирования Windows и управляющие плоскости PowerShell**. Новые возможности могут быть обнаружены в системе System Insights, они также могут воспользоваться преимуществами пользовательских расписаний и действий по исправлению.

## <a name="manage-new-capabilities"></a>Управление новыми возможностями
- [Узнайте](add-remove-update-capabilities.md) , как добавлять, удалять и обновлять возможности с помощью PowerShell.

## <a name="develop-a-capability"></a>Разработка возможностей
Используйте следующие ресурсы, чтобы приступить к написанию собственных пользовательских возможностей.
- [Сведения](data-sources.md) об источниках данных, которые можно отслеживать.
- [Скачайте](https://www.nuget.org/packages/Microsoft.WindowsServer.SystemInsights/) пакет NuGet для System Insights, который содержит классы и интерфейсы, необходимые для создания возможности.
- Дополнительные сведения о классах и интерфейсах System Insights [см](/dotnet/api/microsoft.systeminsights.capability) . в документации по API.
- [Используйте](https://aka.ms/systeminsights-samplecapability) пример функции System Insights, чтобы приступить к работе. В этом примере показано, как зарегистрировать возможность, указать источники данных, которые необходимо получить, и начать анализ системных данных.

>[!NOTE]
>Это функция предварительной версии. Его можно изменить, добавив новые функции и добавив отзывы.

## <a name="additional-references"></a>Дополнительные ссылки
Дополнительные сведения о System Insights см. в следующих ресурсах:

- [Обзор системной аналитики](overview.md)
- [Общие сведения о возможностях](understanding-capabilities.md)
- [Управление возможностями](managing-capabilities.md)
- [Добавление, удаление и обновление возможностей](add-remove-update-capabilities.md)
- [Вопросы и ответы по System Insights](faq.md)