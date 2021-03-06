---
description: Дополнительные сведения см. в статье предоставление пользователям в другой организации доступа к приложениям и службам, поддерживающим утверждения.
ms.assetid: de7e1e4a-f96d-4b59-ac9b-f65f5d37a96f
title: Предоставление пользователям другой организации доступа к вашим приложениям и службам с поддержкой утверждений
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: cf3dcbd1a8c6d14e4866e33e6fab685489df1d45
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049432"
---
# <a name="provide-users-in-another-organization-access-to-your-claims-aware-applications-and-services"></a>Предоставление пользователям другой организации доступа к вашим приложениям и службам с поддержкой утверждений


Если вы являетесь администратором в организации партнера по ресурсам в службы федерации Active Directory (AD FS) \( AD FS \) и у вас есть цель развертывания для предоставления федеративного доступа для пользователей в другой организации \( , организация партнера по учетным записям \) может использовать \- приложение, поддерживающее утверждения, или веб- \- службу, которая находится в вашей организации в \( организации партнера по ресурсам \) :

-   Федеративные пользователи в вашей организации и в организациях, которые настроили доверие Федерации к \( партнерским организациям Организации, \) могут получить доступ к AD FS защищенному приложению или службе, размещенной в вашей организации. Дополнительные сведения см. в разделе [Federated Web SSO Design](Federated-Web-SSO-Design.md).

    Например, в компании Fabrikam может потребоваться предоставить ее сотрудникам федеративный доступ к веб-службам, размещенным в Contoso.

-   Федеративные пользователи, которые не имеют прямой связи с доверенной организацией \( , например отдельными клиентами \) , которые вошли в хранилище атрибутов, размещенное в сети периметра, могут получить доступ к нескольким AD FS \- защищенным приложениям, которые также размещаются в сети периметра, за счет однократного входа с клиентских компьютеров, расположенных в Интернете. Другими словами, когда учетные записи клиентов размещают в сети периметра для обеспечения доступа к приложениям или службам, клиенты, сведения о которых находятся в хранилище атрибутов, могут получать доступ к одному или нескольким приложениям или службам в сети периметра путем однократного входа. Дополнительные сведения см. в разделе [Web SSO Design](Web-SSO-Design.md).

    Например, Fabrikam может потребоваться, чтобы у своих клиентов был \- \- доступ единого \( входа \) для нескольких приложений или служб, размещенных в сети периметра.

Для выполнения этой задачи развертывания необходимы следующие компоненты.

-   **Службы \( домен Active Directory AD DS \) :** сервер федерации партнера по ресурсам должен быть присоединен к домену Active Directory.

-   **DNS периметра:** DNS-сервер системы доменных имен \( \) должен содержать простую \( \) запись ресурса a, чтобы клиентские компьютеры могли нахождение сервера федерации партнера по ресурсам и веб-сервера. DNS-сервер может содержать другие записи DNS, которые также являются обязательными в сети периметра. Дополнительные сведения см. в разделе [Требования к разрешению имен для серверов федерации](Name-Resolution-Requirements-for-Federation-Servers.md).

-   **Сервер федерации партнера по ресурсам:** Сервер федерации партнера по ресурсам проверяет маркеры AD FS, отправляемые партнерами по учетным записям. Обнаружение партнера по учетным записям выполняется через этот сервер федерации. Дополнительные сведения см. в разделе [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md).

-   **Веб-сервер.** На веб-сервере может находиться веб-приложение или веб-служба. Веб-сервер подтверждает получение допустимых маркеров AD FS от федеративных пользователей перед тем, как разрешить доступ к защищенному веб-приложению или веб-службе.

    С помощью Windows Identity Foundation \( WIF \) можно разрабатывать веб-приложение или службу таким образом, чтобы они принимали запросы на вход федеративных пользователей, выполняемые с помощью любого стандартного метода входа в систему, например имя пользователя и пароль.

После просмотра сведений в связанных разделах можно приступить к развертыванию этой цели, выполнив действия, описанные в [контрольном списке ниже: реализация проектирования федеративного единого входа в Интернете](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md) и [Контрольный список: реализация разработки единого входа в Интернете](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md).

На следующем рисунке показаны все необходимые компоненты для этого AD FS цели развертывания.

![доступ к вашим утверждениям](media/75358b16-2a6f-4e16-9cc4-b0e614480305.gif)

## <a name="see-also"></a>См. также:
[Руководство по разработке служб федерации Active Directory в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
