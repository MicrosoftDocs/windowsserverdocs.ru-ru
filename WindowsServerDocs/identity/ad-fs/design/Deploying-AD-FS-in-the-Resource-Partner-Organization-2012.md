---
ms.assetid: 39acccd9-0402-49ca-8ce1-b239e1e7e455
title: "Развертывание AD FS в организации партнера по ресурсам"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a20fab1cca4c33485fd599de5525c7a718e9598e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-ad-fs-in-the-resource-partner-organization"></a>Развертывание AD FS в организации партнера по ресурсам

>Область применения: Windows Server 2012

The resource partner organization in Active Directory Federation Services \(AD FS\) represents the organization whose Web servers may be protected by a resource\-side federation server. The federation server at the resource partner uses the security tokens that are produced by the account partner to provide claims to the Web servers that are located in the resource partner.  
  
In scenarios in which you need to provide access to federated services or applications to many different users—when some users reside in different organizations—you can configure the resource federation server so that you can deploy multiple account partners.  
  
For more information about how to set up and configure a resource partner organization, see [Checklist: Configuring the Resource Partner Organization](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md).  
  
## <a name="in-this-section"></a>В этом разделе  
  
-   [Сведения о роли сервера федерации в организации партнера по ресурсам](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)  
  
-   [Сведения о роли прокси-сервера федерации в организации партнера по ресурсам](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)  
  
-   [Определение стратегии работы с федеративными приложениями в организации партнера по ресурсам](Determine-Your-Federated-Application-Strategy-in-the-Resource-Partner.md)  
  

## <a name="see-also"></a>См. также:
[Руководство по разработке служб AD FS в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
