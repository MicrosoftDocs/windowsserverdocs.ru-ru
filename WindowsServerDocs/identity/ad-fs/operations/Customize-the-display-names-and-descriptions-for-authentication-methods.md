---
description: 'Дополнительные сведения: Настройка отображаемых имен и описаний для методов проверки подлинности'
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: Настройка отображаемых имен и описаний для методов проверки подлинности
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 0b4c094aec3bf36d00074a93753e675d0d642e9f
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97039902"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>Настройка отображаемых имен и описаний для методов проверки подлинности

Чтобы настроить отображаемые имена и описание методов проверки подлинности, можно использовать командлет `Set-AdfsAuthenticationProviderWebContent` PowerShell.  Чтобы использовать этот командлет, сначала необходимо получить имя метода проверки подлинности, который вы хотите настроить.  Это можно сделать с помощью `Get-AdfsGlobalAuthenticationPolicy`.  В приведенном ниже примере показано, что на странице входа \- отображается следующее: "войти с использованием сертификата X. 509".  Мы хотим упростить текст для пользователей.

![Настройка DisplayName](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)

Поэтому сначала мы получаем имя метода проверки подлинности, а затем изменяем отображаемый текст.

```powershell
Get-AdfsGlobalAuthenticationPolicy

AdditionalAuthenticationProvider  : {}
DeviceAuthenticationEnabled   : False
PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}
PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}
WindowsIntegratedFallbackEnabled  : True

Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"
 ```

![Настройка DisplayName](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)

Теперь мы видим, что сообщение изменилось.

![Настройка DisplayName](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)

## <a name="additional-references"></a>Дополнительная справка

[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
