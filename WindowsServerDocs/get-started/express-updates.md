---
title: Экспресс-обновления для Windows Server 2016 снова включены в обновлении за ноябрь 2018 г.
description: Сведения об экспресс-обновлениях в Windows Server 2016.
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.date: 08/07/2020
ms.openlocfilehash: e35f2d8c80ab31f85dc16d3b8f9b37af3ed105ed
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950320"
---
# <a name="express-updates-for-windows-server-2016-re-enabled-for-november-2018-update"></a>Экспресс-обновления для Windows Server 2016 снова включены в обновлении за ноябрь 2018 г.

> Область применения. Windows Server 2016

Начиная со вторника обновлений, 13 ноября 2018 года, команда разработчиков Windows будет снова публиковать экспресс-обновления для Windows Server 2016. Выпуск экспресс-обновлений для Windows Server 2016 был остановлен в середине 2017 года после обнаружения значительной проблемы, препятствовавшей правильной установке обновлений. Хотя проблема была устранена в ноябре 2017 года, команда разработчиков обновлений применила традиционный подход к публикации пакетов экспресс-обновлений, чтобы большинство клиентов установило на свои серверы обновление от 14 ноября 2017 года ([KB4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) и больше не сталкивалось с этой проблемой.

Системным администраторам WSUS и Microsoft Endpoint Configuration Manager следует знать, что в ноябре 2018 года снова доступны два пакета обновления Windows Server 2016: полное обновление и экспресс-обновление. Системным администраторам, которые хотят использовать экспресс-обновление для серверных сред, необходимо убедиться, что на устройстве установлено полное обновление за 14 ноября 2017 года ([KB4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)). Это необходимо для правильной установки экспресс-обновления. При попытке установить экспресс-обновление на любое устройство, на котором не устанавливались обновления с 14 ноября 2017 года ([KB4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)), вы увидите бесконечный цикл повторяющихся ошибок, который использует пропускную способность и ресурсы ЦП.  Чтобы вывести устройство из этого состояния, системному администратору нужно остановить отправку экспресс-обновления и отправить последнее полное обновление. Это остановит цикл ошибок.

С 13 ноября 2018 года клиенты экспресс-обновлений увидят немедленное сокращение размера пакетов для системы управления и конечных точек Windows Server 2016.