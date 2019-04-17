---
ms.assetid: 8c3536b7-d091-4ee6-ad04-24713f070862
title: "Развертывание AD FS в организации партнера по учетным записям"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5b4ba00aa9fed1022d9c0137d05ac6240b44b276
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>Развертывание AD FS в организации партнера по учетным записям

>Область применения: Windows Server 2016, Windows Server 2012 R2

An account partner in Active Directory Federation Services \(AD FS\) represents the organization in the federation trust relationship that physically stores user accounts in a supported attribute store. For more information about which attribute stores are supported, see [The Role of Attribute Stores](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md).  
  
The federation server in the account partner organization authenticates local users and creates security tokens that are used by the resource partner in making authorization decisions. Relying parties such as Web sites and Web services are then able to easily register themselves with the federation server and consume issued tokens for authentication and access control.  
  
In scenarios in which you need to provide your users with access to multiple federated applications or services—when each application or service is hosted by a different organization—you can configure the account partner federation server so that you can deploy multiple relying parties.  
  
For more information about how to set up and configure an account partner organization, see [Checklist: Configuring the Account Partner Organization](../../ad-fs/deployment/Checklist--Configuring-the-Account-Partner-Organization.md).  
  
## <a name="in-this-section"></a>В этом разделе  
  
-   [Сведения о роли сервера федерации в партнера по учетным записям](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)  
  
-   [Сведения о роли прокси-сервера федерации в организации партнера по учетной записи](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)  
  
-   [Prepare Client Computers in the Account Partner](Prepare-Client-Computers-in-the-Account-Partner.md)  
  
## <a name="see-also"></a>См. также:
[Руководство по разработке служб AD FS в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
