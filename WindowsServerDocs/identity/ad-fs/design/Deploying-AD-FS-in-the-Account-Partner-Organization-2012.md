---
description: 'Дополнительные сведения: развертывание AD FS в организации партнера по учетным записям'
ms.assetid: 9aaca9c5-ce44-495c-aad6-61aede87a83f
title: Развертывание служб федерации Active Directory в партнерской организации по учетным записям
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: e9617b737c929c029a103bbd6054c0dbc33d9eb4
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97044742"
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>Развертывание служб федерации Active Directory в партнерской организации по учетным записям

Партнер по учетным записям в службы федерации Active Directory (AD FS) \( AD FS \) представляет организацию в отношении доверия федерации, которая физически хранит учетные записи пользователей в поддерживаемом хранилище атрибутов. Дополнительные сведения о поддерживаемых хранилищах атрибутов см. в разделе [роль хранилищ атрибутов](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md).

Сервер федерации в организации партнера по учетным записям выполняет проверку подлинности локальных пользователей и создает маркеры безопасности, используемые партнером по ресурсам для принятия решений об авторизации. Затем проверяющие стороны, такие как веб-сайты и веб-службы, могут легко зарегистрироваться на сервере федерации и использовать выданные маркеры для проверки подлинности и контроля доступа.

В сценариях, в которых необходимо предоставить пользователям доступ к нескольким федеративным приложениям или службам. Если каждое приложение или служба размещается в другой организации, можно настроить сервер федерации партнера по учетным записям, чтобы можно было развернуть несколько проверяющих сторон.

Подробнее об установке и настройке партнерской организации по учетным записям см. в разделе [Checklist: Configuring the Account Partner Organization](../../ad-fs/deployment/Checklist--Configuring-the-Account-Partner-Organization.md).

## <a name="in-this-section"></a>В этом разделе

-   [Сведения о роли сервера федерации в организации партнера по учетным записям](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)

-   [Сведения о роли прокси-сервера федерации в организации партнера по учетным записям](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)

-   [Подготовка клиентских компьютеров к работе с партнером по учетным записям](Prepare-Client-Computers-in-the-Account-Partner.md)

## <a name="see-also"></a>См. также:
[Руководство по разработке служб федерации Active Directory в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
