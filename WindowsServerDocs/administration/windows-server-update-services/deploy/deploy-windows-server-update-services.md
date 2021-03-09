---
title: Развертывание служб Windows Server Update Services
description: Узнайте о службе Windows Server Update Service (WSUS), в т. ч. о процессе развертывания (ниже приведены ссылки на соответствующие разделы).
ms.topic: how-to
ms.assetid: 2708f6b2-4252-4b8f-9b7e-84c9b4222075
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: efe6a83f2e9fbd80d2d387238ec28b6ae0a125b9
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101827375"
---
# <a name="deploy-windows-server-update-services"></a>Развертывание служб Windows Server Update Services

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Службы Windows Server Update Services (WSUS) позволяют ИТ-администраторам развертывать новейшие обновления продуктов Майкрософт. WSUS — это роль сервера Windows Server, которую можно установить для распространения обновлений и управления ими. Сервер служб WSUS может быть источником обновлений для других серверов WSUS в организации. Сервер WSUS, действующий как источник обновлений, называется вышестоящим сервером.

При реализации служб WSUS хотя бы один сервер служб WSUS в сети должен быть подключен к Центру обновления Майкрософт для получения информации о доступных обновлениях. В зависимости от безопасности сети и ее конфигурации вы можете определить, сколько других серверов напрямую подключено к Центру обновления Майкрософт.

Это руководство содержит базовые сведения о планировании развертывания службы Windows Server Update Service.

-   [Планирование развертывания WSUS](../plan/plan-your-wsus-deployment.md)

-   [Шаг 1. Установка роли сервера WSUS](1-install-the-wsus-server-role.md)

-   [Шаг 2. Настройка служб WSUS](2-configure-wsus.md)

-   [Шаг 3. Утверждение и развертывание обновлений в службах WSUS](3-approve-and-deploy-updates-in-wsus.md)

-   [Шаг 4. Настройка параметров групповой политики для автоматического обновления](4-configure-group-policy-settings-for-automatic-updates.md)
