---
description: Дополнительные сведения см. в статье Планирование условного доступа на основе устройств в локальной среде.
ms.assetid: c5eb3fa0-550c-4a2f-a0bc-698b690c4199
title: Планирование локального условного доступа на основе устройств
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 8301cb1396785d56d81e08e2ad3d52ee4d66d887
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97043312"
---
# <a name="plan-device-based-conditional-access-on-premises"></a>Планирование локального условного доступа на основе устройств


В этом документе описываются политики условного доступа на основе устройств в гибридном сценарии, где локальные каталоги подключены к Azure AD с помощью Azure AD Connect.

## <a name="ad-fs-and-hybrid-conditional-access"></a>AD FS и гибридный условный доступ

AD FS реализует локальный компонент политик условного доступа в гибридном сценарии.  Когда вы регистрируете устройства в Azure AD для условного доступа к облачным ресурсам, функция обратной записи Azure AD Connect устройства делает сведения о регистрации устройства доступными локально для использования и применения политик AD FS.  Таким образом, у вас есть единообразный подход к политикам управления доступом как к локальным, так и к облачным ресурсам.

![условный доступ](media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)

### <a name="types-of-registered-devices"></a>Типы зарегистрированных устройств
Существует три типа зарегистрированных устройств, которые представляются как объекты устройств в Azure AD и могут использоваться для условного доступа с AD FS локально.

| Описание |Добавить рабочую или учебную учетную запись  |Присоединение к Azure AD  |Присоединение к домену Windows 10 |
| --- | --- |--- | --- |
|Описание    |  Пользователи могут интерактивно добавлять свою рабочую или учебную учетную запись на устройство BYOD.  **Примечание.** Добавление рабочей или учебной учетной записи — это замена Workplace Join в Windows 8 или 8.1 | Пользователи присоединяются к Azure AD с рабочего устройства Windows 10.|Устройства, присоединенные к домену Windows 10, автоматически регистрируются в Azure AD.|
|Как пользователи входят на устройство     |  Нет имени входа в систему Windows в качестве рабочей или учебной учетной записи.  Вход с помощью учетная запись Майкрософт. |      | Войдите в Windows как учетную запись (рабочую или учебную), которая зарегистрировала устройство. | Вход с использованием учетной записи AD.|
|Управление устройствами | Политики MDM (с дополнительной регистрацией в Intune) | Политики MDM (с дополнительной регистрацией в Intune) | Групповая политика, Configuration Manager |
|Тип доверия Azure AD|Присоединено к рабочему месту|присоединение к Azure AD;|Присоединен к домену |
|Расположение параметров W10 | Параметры > учетные записи > учетной записи > Добавление рабочей или учебной учетной записи | Параметры > системе > об > присоединиться к Azure AD |   Параметры > системе > о > присоединиться к домену |
|Также доступно для устройств iOS и Android? | Да | Нет | Нет |

Дополнительные сведения о различных способах регистрации устройств см. также в следующих статьях:
* [Устройства под управлением Windows 10 в вашей рабочей области](/azure/active-directory/devices/overview)
* [Настройка устройств Windows 10 для работы](https://jairocadena.com/2016/01/18/setting-up-windows-10-devices-for-work-domain-join-azure-ad-join-and-add-work-or-school-account/) 
 [Присоединение Windows 10 Mobile к Azure Active Directory](/windows/client-management/join-windows-10-mobile-to-azure-active-directory)

### <a name="how-windows-10-user-and-device-sign-on-is-different-from-previous-versions"></a>Как вход пользователя и устройства Windows 10 отличается от предыдущих версий
Для Windows 10 и AD FS 2016 есть некоторые новые аспекты регистрации устройств и проверки подлинности, о которых следует знать (особенно если вы хорошо знакомы с регистрацией устройств и "присоединение к рабочей области" в предыдущих выпусках).

Во-первых, в Windows 10 и AD FS в Windows Server 2016 регистрация устройств и проверка подлинности больше не основываются исключительно на сертификате пользователя X509.  Существует новый и более надежный протокол, обеспечивающий более высокую безопасность и удобство работы пользователей.  Основное различие заключается в том, что для присоединение к домену Windows 10 и присоединение к Azure AD существует сертификат компьютера X509 и новые учетные данные, называемые PRT.  Сведения о нем можно прочитать [здесь](https://jairocadena.com/2016/01/18/how-domain-join-is-different-in-windows-10-with-azure-ad/) и [здесь](https://jairocadena.com/2016/02/01/azure-ad-join-what-happens-behind-the-scenes/).

Во вторых, Windows 10 и AD FS 2016 поддерживают проверку подлинности пользователей с помощью Microsoft Passport for Work, которую можно прочитать [здесь](https://jairocadena.com/2016/03/09/azure-ad-and-microsoft-passport-for-work-in-windows-10/) и [здесь](/windows/security/identity-protection/hello-for-business/hello-identity-verification).

AD FS 2016 обеспечивает эффективное единый вход устройств и пользователей на основе учетных данных PRT и Passport.  С помощью действий, описанных в этом документе, можно включить эти возможности и увидеть их работу.

### <a name="device-access-control-policies"></a>Политики управления доступом к устройствам
Устройства можно использовать в простых AD FS правилах управления доступом, таких как:

- разрешить доступ только с зарегистрированного устройства
- требовать многофакторную проверку подлинности, если устройство не зарегистрировано

Эти правила можно объединять с другими факторами, такими как расположение сетевого доступа и многофакторная проверка подлинности, создавая широкие политики условного доступа, такие как:


- требовать многофакторную проверку подлинности для незарегистрированных устройств, обращающихся извне корпоративной сети, за исключением членов определенной группы или групп

В AD FS 2016 эти политики могут быть настроены специально для того, чтобы требовать определенного уровня доверия устройства: с **проверкой подлинности**, **управляемым** или **соответствующим** образом.

Дополнительные сведения о настройке политик управления доступом AD FS см. [в разделе политики контроля доступа в AD FS](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md).

#### <a name="authenticated-devices"></a>Проверенные устройства
Проверенные устройства — это зарегистрированные устройства, которые не зарегистрированы в MDM (Intune и сторонние МДМС для Windows 10, Intune только для iOS и Android).

Прошедшие проверку подлинности устройства будут иметь **Неуправляемое** AD FS утверждении со значением **false**. (В то время как устройства, которые не зарегистрированы вообще, это утверждение отсутствует.)  Прошедшие проверку подлинности устройства (и все зарегистрированные устройства) будут иметь AD FS утверждению со значением **true**.

#### <a name="managed-devices"></a>Управляемые устройства:

Управляемые устройства — это зарегистрированные устройства, регистрируемые в MDM.

На управляемых устройствах будет присвоено утверждение AD FS с помощью значения **true**.

#### <a name="devices-compliant-with-mdm-or-group-policies"></a>Устройства, совместимые (с MDM или групповыми политиками)
Соответствующие устройства — это зарегистрированные устройства, которые не только зарегистрированы в MDM, но и соответствуют политикам MDM. (Сведения о соответствии исходят от MDM и записываются в Azure AD.)

Соответствующие требованиям устройства будут иметь **AD FS** утверждению со значением **true**.

Полный список утверждений для устройств AD FS 2016 и условного доступа см. в [справочнике](#reference).


## <a name="reference"></a>Справочник
#### <a name="complete-list-of-new-ad-fs-2016-and-device-claims"></a>Полный список новых AD FS 2016 и утверждений устройств

* https://schemas.microsoft.com/ws/2014/01/identity/claims/anchorclaimtype
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/implicitupn
* https://schemas.microsoft.com/2014/03/psso
* https://schemas.microsoft.com/2015/09/prt
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn
* https://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid
* https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name
* https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname
* https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid
* https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid
* https://schemas.microsoft.com/2012/01/devicecontext/claims/displayname
* https://schemas.microsoft.com/2012/01/devicecontext/claims/identifier
* https://schemas.microsoft.com/2012/01/devicecontext/claims/ostype
* https://schemas.microsoft.com/2012/01/devicecontext/claims/osversion
* https://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged
* https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser
* https://schemas.microsoft.com/2014/02/devicecontext/claims/isknown
* https://schemas.microsoft.com/2014/02/deviceusagetime
* https://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant
* https://schemas.microsoft.com/2014/09/devicecontext/claims/trusttype
* https://schemas.microsoft.com/claims/authnmethodsreferences
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path
* https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork
* https://schemas.microsoft.com/2012/01/requestcontext/claims/client-request-id
* https://schemas.microsoft.com/2012/01/requestcontext/claims/relyingpartytrustid
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-ip
* https://schemas.microsoft.com/2014/09/requestcontext/claims/userip
* https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod
