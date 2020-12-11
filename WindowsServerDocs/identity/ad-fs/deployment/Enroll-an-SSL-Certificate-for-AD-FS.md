---
description: Дополнительные сведения см. в статье регистрация SSL-сертификата для AD FS
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: Регистрация SSL-сертификата для AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 398be855788314ca54b634db445338e45cd0f84d
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97044092"
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>Регистрация SSL-сертификата для AD FS

Службы федерации Active Directory (AD FS) \( AD FS \) требуется сертификат для \( \) проверки подлинности SSL-сервера на каждом сервере федерации в ферме серверов федерации. Один и тот же сертификат можно использовать на каждом сервере федерации в ферме. Сертификат и его закрытый ключ должны быть доступны. Например, если сертификат и его закрытый ключ находятся в PFX-файле, то можно импортировать этот файл непосредственно в мастер настройки служб федерации Active Directory. Этот SSL-сертификат должен содержать указанные ниже данные.

1.  Имя субъекта и альтернативное имя субъекта должны содержать имя службы федерации, например fs.contoso.com.

2.  Альтернативное имя субъекта должно содержать значение **enterpriseregistration** , за которым следует имя субъекта-пользователя с \( \) суффиксом UPN вашей организации, например **enterpriseregistration.Corp.contoso.com**.

    > [!WARNING]
    > Укажите альтернативное имя субъекта, если вы планируете включить службу регистрации устройств \( DRS \) для Workplace JOIN.

> [!IMPORTANT]
> Если в вашей организации используется несколько суффиксов имени участника-пользователя и вы планируете включить DRS, SSL-сертификат должен содержать запись альтернативного имени субъекта для каждого суффикса.

## <a name="see-also"></a>См. также:
[Развертывание AD FS](../../ad-fs/AD-FS-Deployment.md)

[Руководство по развертыванию служб федерации Active Directory в Windows Server 2012 R2](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)

[Развертывание фермы серверов федерации](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)



