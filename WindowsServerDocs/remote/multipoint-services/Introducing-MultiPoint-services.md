---
title: Основные сведения о службах MultiPoint
description: Содержит общие сведения о службах MultiPoint, способах предоставления общего доступа к системе нескольким пользователям.
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 1cbef744-4661-4ba9-9e2b-0bbd8854fd5c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 663b3d4afade9b4fb459f34120d1e6b18984285a
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997432"
---
# <a name="introducing-multipoint-services"></a>Основные сведения о службах MultiPoint
Роль служб MultiPoint в Windows Server 2016 позволяет нескольким пользователям с собственными независимыми и привычными возможностями Windows совместно использовать один компьютер. Существует несколько способов доступа пользователей к своим сеансам. Один из способов — удаленное взаимодействие с сервером с помощью [приложений удаленного рабочего стола](../remote-desktop-services/clients/remote-desktop-clients.md) с любым устройством. Другой способ — благодаря физическим станциям, подключенным к серверу MultiPoint:

-   Непосредственно к видео портам на компьютере

-   Через специализированные нуль-клиентов USB (также называемых многофункциональными концентраторами USB), а также через аналогичные устройства USB-over-Ethernet.

-   По локальной сети (LAN)

Каждый из этих методов более подробно описан в разделе [станции служб MultiPoint](MultiPoint-services-Stations.md) в этом документе.

В этом документе рассматриваются следующие факторы, которые следует учитывать при планировании развертывания служб MultiPoint.

-   Какие типы настольных компьютеров будут использоваться в системе служб MultiPoint: требуются ли сеансы, виртуальные машины или компьютеры Windows?

-   [Выбор оборудования для системы служб MultiPoint](./select-hardware-mps.md): какие решения должно быть принято?

-   [Требования к оборудованию и рекомендации по производительности](./hardware-and-performance-recommendations.md): какое оборудование требуется для служб MultiPoint?

-   [Планирование сайтов служб MultiPoint](MultiPoint-services-Site-Planning.md). где будут размещаться компьютеры, на которых работают службы MultiPoint и их станции, и как они будут настроены?

-   [Рекомендации по сети и учетные записи пользователей](Network-Considerations-and-User-Accounts.md). Сетевая среда, в которой развернута система служб MultiPoint, может влиять на управление учетными записями пользователей. Что такое сетевая среда? Как будут управляться учетными записями пользователей?

-   [Хранение файлов с помощью служб MultiPoint](Storing-Files-with-MultiPoint-services.md): где будут храниться файлы пользователей и как они будут доступны?

-   [Контрольный список действий, выполняемых перед развертыванием](Predeployment-Checklist.md)