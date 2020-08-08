---
ms.assetid: 1df78c2a-5054-4b54-8310-c48ea62e6e0b
title: Настраиваемые сообщения об ошибках для страницы входа AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 91d9e0e5ba0a0272c1efc820578fb6547a14abc8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956441"
---
# <a name="custom-error-messages-for-ad-fs-sign-in-page"></a>Настраиваемые сообщения об ошибках для страницы входа AD FS

Можно настроить пользовательские сообщения об ошибках специально для вашей организации. На следующей иллюстрации показаны настроенное описание страницы ошибок и универсальное сообщение об ошибке. Используйте следующие командлеты Windows PowerShell для настройки сообщений об ошибках.

![настраиваемая ошибка](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom3.png)

## <a name="customize-the-error-page-description"></a>Настройка описания страницы ошибок

Чтобы настроить описание страницы ошибки, используйте следующий командлет и синтаксис Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description"
```

## <a name="customize-a-generic-error-message"></a>Настройка универсального сообщения об ошибке
Чтобы настроить общее сообщение об ошибке, используйте следующий командлет и синтаксис Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -ErrorPageGenericErrorMessage "This is a generic error message.  Contact Contoso IT for assistance."
```

## <a name="customize-an-authorization-error-message"></a>Настройка сообщения об ошибке авторизации
Чтобы настроить сообщение об ошибке авторизации, используйте следующий командлет и синтаксис Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -ErrorPageAuthorizationErrorMessage "You have received an Authorization error.  Contact Contoso IT for assistance."
```

## <a name="customize-a-device-authentication-error-message"></a>Настройка сообщения об ошибке аутентификации устройства
Чтобы настроить сообщение об ошибке проверки подлинности устройства, используйте следующий командлет и синтаксис Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -ErrorPageDeviceAuthenticationErrorMessage "Your device is not authorized.  Contact Contoso IT for assistance."
```

## <a name="customize-a-support-email-error-message"></a>Настройка сообщения об ошибке с указанием электронного адреса службы поддержки
Адрес электронной почты службы поддержки можно настроить в AD FS. Если этот параметр настроен, AD FS автоматически отображает ссылку для отправки сведений об ошибке конечным пользователям по электронной почте.

Чтобы настроить сообщение об ошибке поддержки электронной почты, используйте следующий командлет и синтаксис Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -ErrorPageSupportEmail  "admin@contoso.com"
```

## <a name="customize-a-relying-party-authorization-message"></a>Настройка сообщения авторизации проверяющей стороны
Сообщение об ошибке авторизации проверяющей стороны можно настроить в AD FS.

Чтобы настроить сообщение об ошибке проверяющей стороны, используйте следующий командлет и синтаксис Windows PowerShell.

```powershell
Set-AdfsRelyingPartyWebContent -Name fedpassive -ErrorPageAuthorizationErrorMessage "<p> You need to be a member of Security Auditors to access this site. Click <A href='http://accessrequest/'>here</A> for more information.</p>"
```

## <a name="additional-references"></a>Дополнительная справка

[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
