---
ms.assetid: 41d6b897-1e72-4522-aad6-eece1154a154
title: Развертывание устаревших AD FS в организации партнера по ресурсам
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 63afcbf825aadcc8207793e6e7ccb3cdc48cacbb
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87863797"
---
# <a name="deploying-legacy-ad-fs-in-the-resource-partner-organization"></a>Развертывание устаревших AD FS в организации партнера по ресурсам

Организация партнера по ресурсам в службы федерации Active Directory (AD FS) \( AD FS \) представляет организацию, веб-серверы которой могут быть защищены \- сервером федерации на стороне ресурсов. Сервер федерации в партнере по ресурсам использует маркеры безопасности, созданные партнером по учетным записям для предоставления утверждений для веб-серверов, которые находятся в партнере по ресурсам.  
  
В сценариях, в которых необходимо предоставить доступ к федеративным службам или приложениям многим разным пользователям — когда некоторые пользователи находятся в разных организациях, можно настроить сервер федерации ресурсов, чтобы можно было развернуть нескольких партнеров по учетным записям.  
  
Дополнительные сведения об установке и настройке партнерской организации по ресурсам см. в разделе [Checklist: Configuring the Resource Partner Organization](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md).  
  
## <a name="in-this-section"></a>Содержание раздела  
  
-   [Сведения о роли сервера федерации в организации партнера по ресурсам](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)  
  
-   [Сведения о роли прокси-сервера федерации в организации партнера по ресурсам](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)  
  
-   [Определение стратегии работы с федеративными приложениями у партнера по ресурсам](Determine-Your-Federated-Application-Strategy-in-the-Resource-Partner.md)  
  

## <a name="see-also"></a>См. также:
[Руководство по разработке служб федерации Active Directory в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
