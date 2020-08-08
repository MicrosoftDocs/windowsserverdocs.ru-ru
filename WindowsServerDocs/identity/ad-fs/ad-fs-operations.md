---
ms.assetid: eefcc989-8763-45ee-8a64-3a97b4397160
title: Операции AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 3fb672d9557e7f10245e8c29ea1585cf9f4aadf9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953191"
---
# <a name="ad-fs-operations"></a>Операции AD FS



Этот документ содержит список всех операций с документацией для AD FS.

## <a name="service-configuration"></a>Конфигурация службы
- [Обновление SSL-сертификатов в AD FS и WAP 2016](./operations/manage-ssl-certificates-ad-fs-wap.md)
- [Средство ускоренного восстановления AD FS](../ad-fs/operations/AD-FS-Rapid-Restore-Tool.md)
- [Настройка альтернативной привязки имени узла для проверки подлинности сертификата в AD FS](../ad-fs/operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
- [Добавление хранилища атрибутов](../ad-fs/operations/Add-an-Attribute-Store.md)
- [Настройка заголовков ответов безопасности HTTP с помощью AD FS 2019](../ad-fs/operations/customize-http-security-headers-ad-fs.md)
- [Делегирование доступа к командлету Powershell AD FS пользователям без прав администратора](../ad-fs/operations/delegate-ad-fs-pshell-access.md)
- [Точная настройка SQL и задержка адресов](../ad-fs/operations/adfs-sql-latency.md)
- [Группы доступности AlwaysOn](../ad-fs/operations/ad-fs-always-on.md)


## <a name="authentication-configuration"></a>Настройка проверки подлинности
### <a name="strong-authentication-mfa--password-less"></a>Строгая проверка подлинности (MFA) & без пароля
- [Настройка внешних поставщиков проверки подлинности в качестве первичного в AD FS (2019 или более поздней версии)](../ad-fs/operations/Additional-Authentication-Methods-AD-FS.md)
- [Настройка AD FS (2016 или более поздней версии) и Azure MFA](./operations/configure-ad-fs-and-azure-mfa.md)
- [Настройка дополнительных методов проверки подлинности для AD FS](../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)

### <a name="lockout-protection"></a>Защита от блокировки
- [Настройка защиты мягкой блокировки экстрасети AD FS](../ad-fs/operations/Configure-AD-FS-Extranet-Soft-Lockout-Protection.md)
- [Настройка защиты интеллектуальной блокировки экстрасети AD FS](../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md)
- [Настройка заблокированных IP-адресов экстрасети AD FS](../ad-fs/operations/Configure-AD-FS-Banned-IP.md)

### <a name="policy-configuration"></a>Настройка политики
- [Настройка политик аутентификации](../ad-fs/operations/Configure-Authentication-Policies.md)
- [Настройка альтернативного идентификатора входа](../ad-fs/operations/Configuring-Alternate-Login-ID.md)
- [Настройка поведения входа в систему Azure AD для работы с AD FS политикой](../ad-fs/operations/AD-FS-Prompt-Login.md)

### <a name="kerberos--certificate-authentication"></a>Проверка подлинности Kerberos & сертификата
- [Включение AD DS утверждений & составной проверки подлинности Kerberos в AD FS](../ad-fs/operations/AD-FS-Compound-Authentication-and-AD-DS-claims.md)
- [Настройка AD FS для проверки подлинности сертификата пользователя](../ad-fs/operations/Configure-User-Certificate-Authentication.md)
- [Настройка альтернативной привязки имени узла для проверки подлинности сертификата в AD FS](../ad-fs/operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)


### <a name="device"></a>Устройство
- [Элементы управления аутентификацией устройств в AD FS](../ad-fs/operations/device-authentication-controls-in-AD-FS.md)


## <a name="authorization-configuration"></a>Настройка авторизации
- [Настройка политик контроля доступа в AD FS](../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)
- [Настройка локального условного доступа на основе устройств](../ad-fs/operations/Configure-Device-based-Conditional-Access-on-Premises.md)

## <a name="rpt--cpt-configuration"></a>RPT & конфигурация КПТ
- [Настройка AD FS для аутентификации пользователей, хранящихся в каталогах LDAP](../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)
- [Настройка правил для утверждения](../ad-fs/operations/Configure-Claim-Rules.md)
- [Создание отношения доверия с поставщиком утверждений](../ad-fs/operations/Create-a-Claims-Provider-Trust.md)
- [Создание отношения доверия с проверяющей стороной, не поддерживающей утверждения](../ad-fs/operations/Create-a-Non-Claims-Aware-Relying-Party-Trust.md)
- [Создание отношений доверия с проверяющей стороной](../ad-fs/operations/Create-a-Relying-Party-Trust.md)
- [Настройка AD FS для работы с агрегированным поставщиком Федерации (например, редкими)](../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)

## <a name="sign-in-experience-configuration"></a>Конфигурация интерфейса входа
- [Настройка параметров единого входа AD FS 2016](./operations/ad-fs-single-sign-on-settings.md)
- [Настройка AD FS страничного входа в систему](../ad-fs/operations/AD-FS-paginated-sign-in.md)
- [Настройка AD FS пользовательской настройки входа](../ad-fs/operations/AD-FS-user-sign-in-customization.md)
- [Настройка AD FS для отправки утверждений об истечении срока действия пароля](../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)
- [Настройка аутентификации в интрасети на основе форм для устройств, не поддерживающих WIA](../ad-fs/operations/Configure-intranet-forms-based-authentication-for-devices-that-do-not-support-WIA.md)

## <a name="other"></a>Другие
- [Присоединение к рабочей области с любого устройства для единого входа и эффективная двухфакторная аутентификация в приложениях компании](../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [Управление рисками для уязвимых приложений с помощью дополнительной многофакторной аутентификации](../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
- [Управление рисками с использованием условного управления доступом](../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)
- [Настройка среды лаборатории AD FS](../ad-fs/operations/Set-up-an-AD-FS-lab-environment.md)
- [Пошаговое руководство. Управление рисками с помощью дополнительной многофакторной проверки подлинности для конфиденциальных приложений](../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
- [Пошаговое руководство. Управление рисками с использованием условного управления доступом](../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)
- [Пошаговое руководство: Присоединение к рабочему месту с устройства Windows](../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)
- [Пошаговое руководство: Присоединение к рабочему месту с устройства iOS](../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)


