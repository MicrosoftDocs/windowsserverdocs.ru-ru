---
description: 'Дополнительные сведения: Настройка отображаемых имен и описаний для методов проверки подлинности'
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: Настройка отображаемых имен и описаний для методов проверки подлинности
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 33a264bc2230087d89a88c70e29edb76e3a09ed6
ms.sourcegitcommit: 6a62d736e4d9989515c6df85e2577662deb042b6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/11/2021
ms.locfileid: "98103806"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>Настройка отображаемых имен и описаний для методов проверки подлинности

Чтобы настроить отображаемые имена и описания методов проверки подлинности, можно использовать `Set-AdfsAuthenticationProviderWebContent` командлет PowerShell.  Чтобы использовать этот командлет, сначала необходимо получить имя метода проверки подлинности, который вы хотите настроить.  Это можно сделать с помощью `Get-AdfsGlobalAuthenticationPolicy`.  В приведенном ниже примере показано, что на странице входа \- отображается следующее: "войти с использованием сертификата X. 509".  Мы хотим упростить текст для пользователей.

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

![Снимок экрана, показывающий, как получить имя метода проверки подлинности и изменить отображаемый текст.](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)

Теперь мы видим, что сообщение изменилось.

![Снимок экрана, на котором показано, что отображаемое сообщение изменилось.](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)

## <a name="additional-references"></a>Дополнительная справка

[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
