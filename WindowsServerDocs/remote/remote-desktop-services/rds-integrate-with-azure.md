---
title: RDS — интеграция со службами Azure
description: Узнайте, как интегрировать службы удаленных рабочих столов в среду Azure.
ms.author: elizapo
ms.date: 08/18/2017
ms.topic: article
author: lizap
ms.openlocfilehash: 410a08d5b222fe0888c77ca6eac061a302730619
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948887"
---
# <a name="remote-desktop-services---integrating-with-azure-services"></a>Службы удаленных рабочих столов — интеграция со службами Azure

Windows Server 2016 сочетает в себе возможности эффективной и безопасной доставки рабочих столов и приложений с помощью служб удаленных рабочих столов и гибкие масштабируемые службы, предоставляемые Microsoft Azure. Развертывание служб удаленных рабочих со службами Azure позволяет сократить затраты на обслуживание инфраструктуры для локальных серверов, повысить стабильность за счет использования служб Azure, обеспечивающих высокий уровень доступности, улучшить безопасность с помощью многофакторной проверки подлинности и придать удобство работе пользователей благодаря использованию существующих удостоверений для доступа к ресурсам в RDS.

Сведения об интеграции Azure в развертывание удаленного рабочего стола см. в следующих статьях:

- [Использование Многофакторной идентификации с RDS](/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)
- [Интеграция доменных служб Azure AD со средой RDS](rds-azure-adds.md)
- [Публикация удаленного рабочего стола с помощью прокси-сервера приложений Azure AD](/azure/active-directory/application-proxy-publish-remote-desktop)

Сведения о том, как эти службы способны упростить архитектуру развертывания удаленного рабочего стола, см. в разделе об [архитектуре RDS с уникальными ролями PaaS в Azure](desktop-hosting-logical-architecture.md#rds-architectures-with-unique-azure-paas-roles).