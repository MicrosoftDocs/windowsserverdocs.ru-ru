---
ms.assetid: ddfbbda3-30ca-4537-af12-667efc6f63ff
title: Настройка дополнительных методов проверки подлинности для службы федерации Active Directory
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/26/2019
ms.topic: article
ms.openlocfilehash: 66ef77b46065b87e6df08c63b0fb40ca4453c45b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954260"
---
# <a name="configure-additional-authentication-methods-for-ad-fs"></a>Настройка дополнительных методов проверки подлинности для службы федерации Active Directory

Для многофакторной проверки подлинности (MFA) необходимо выбрать по крайней мере один дополнительный метод проверки подлинности. По умолчанию в службы федерации Active Directory (AD FS) (AD FS) в Windows Server 2012 R2 можно выбрать проверку подлинности с помощью сертификата (иными словами, аутентификация на основе смарт-карт) в качестве дополнительного метода проверки подлинности.

> [!NOTE]
> Выбирая проверку подлинности сертификата, убедитесь в том, что сертификаты смарт-карт представлены в защищенном виде и имеют требование ввода ПИН-кода.

Вы знаете, что Microsoft Azure предоставляет аналогичную функциональность в облаке? Подробнее о [решениях для удостоверений Microsoft Azure](https://aka.ms/m2w274).<p>Создайте гибридное решение для удостоверений в Microsoft Azure:<br /> - [Подробнее о многофакторной идентификации Azure.](https://aka.ms/ey6o9r)<br /> - [Управление удостоверениями для гибридных сред с одним лесом с использованием проверки подлинности в облаке.](https://aka.ms/g1jat8)<br /> - [Управление рисками с помощью дополнительной многофакторной проверки подлинности для конфиденциальных приложений.](https://aka.ms/kt1bbm)

## <a name="microsoft-and-third-party-additional-authentication-methods"></a>Корпорация Майкрософт и сторонние дополнительные методы проверки подлинности
Также можно настроить и включить методы проверки подлинности Майкрософт и сторонних производителей в AD FS в Windows Server 2012 R2. После установки и регистрации в AD FS можно применить MFA в рамках глобальной политики проверки подлинности или для отдельной проверяющей стороны.

Ниже приведен алфавитный список поставщиков Майкрософт и сторонних поставщиков с предложениями многофакторной проверки подлинности, которые в настоящий момент доступны для службы федерации Active Directory в Windows Server 2012 R2.

|Поставщик|Предложение|Ссылки на дополнительные сведения|
|-|-|-|
|аперсона|Аперсона Адаптивная многофакторная проверка подлинности для единого входа Microsoft ADFS|[Адаптер ADFS Аперсона ASM](https://www.apersona.com/adfs)|
|Циферкор Inc.|Многофакторная проверка подлинности Логинтк для AD FS|[Соединитель AD FS Логинтк](https://www.logintc.com/docs/connectors/adfs.html)|
|Duo Security|Адаптер MFA для AD FS|[Duo для проверки подлинности AD FS](https://duo.com/docs/adfs)|
|футурае|Набор проверки подлинности футурае для AD FS|[Футурае строгая проверка подлинности](https://futurae.com)|
|Компания Gemalto|Службы идентификации и безопасности компании Gemalto|[http://www.gemalto.com/identity](http://www.gemalto.com/identity)|
|inWebo Technologies|Службы корпоративной проверки подлинности inWebo|[Корпоративная проверка подлинности inWebo](http://www.inwebo.com)|
|Login People|API-соединитель Login People MFA для AD FS 2012 R2 (общедоступная бета-версия)|[https://www.loginpeople.com](https://www.loginpeople.com)|
|Корпорация Майкрософт.|Многофакторная проверка подлинности Microsoft Azure|[Пошаговое руководство: управление рисками для уязвимых приложений с помощью дополнительной проверки подлинности Multi-Factor Authentication](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280946(v=ws.11)) (см. шаг 3)|
мидэйе | Поставщик проверки подлинности мидэйе для ADFS | [Мидэйе двухфакторная проверка подлинности с помощью Microsoft Active Directory служба федерации](https://www.mideye.com/support/administrators/documentation/integration/microsoft-adfs/)|
|Okta | Okta MFA для службы федерации Active Directory (AD FS) | [Okta MFA для службы федерации Active Directory (AD FS) (ADFS)](https://help.okta.com/en/prod/Content/Topics/integrations/adfs-okta-int.htm)|
|One Identity| Старлинг 2FA AD FS|[Адаптер AD FS 2FA Старлинг](https://www.oneidentity.com/products/starling-two-factor-authentication/)|
|One Identity| AD FS защитника|[Адаптер AD FS защитника](https://www.oneidentity.com/products/defender/)|
|Ping Identity;|Адаптер Пингид MFA для AD FS|[Адаптер Пингид MFA для AD FS](https://documentation.pingidentity.com/pingid/pingidAdminGuide/index.shtml#pid_c_PingIDforADFSSSO.html)|
|RSA, подразделение безопасности EMC|Агент проверки подлинности RSA SecurID для служб федерации Microsoft Active Directory|[Агент проверки подлинности RSA SecurID для служб федерации Microsoft Active Directory](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)|
|SafeNet, Inc.|Агент службы проверки подлинности SafeNet (SAS) для AD FS|[Служба проверки подлинности SafeNet: руководство по конфигурации агента AD FS](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)|
|секуремфа|Поставщик OTP Секуремфа| [Поставщики многофакторной идентификации ADFS](https://www.securemfa.com/)|
|Swisscom|Служба проверки подлинности Mobile ID и службы подписей|[Служба проверки подлинности Mobile ID](http://swisscom.ch/mid)|
|Symantec|Служба проверки и защиты идентификации Symantec (VIP)|[Служба проверки и защиты идентификации Symantec (VIP)](http://www.symantec.com/vip-authentication-service)|
|Trusona|Важными (незащищенные паролем MFA) и Executive (основы проверки личности)| [Многофакторная идентификация трусона](https://www.trusona.com/solution-overview/)|


## <a name="custom-authentication-method-for-ad-fs-in-windows-server-2012-r2"></a>Пользовательский метод проверки подлинности для AD FS в Windows Server 2012 R2
Теперь мы предоставляем инструкции по созданию собственного метода проверки подлинности для AD FS в Windows Server 2012 R2. Дополнительные сведения см. в разделе [Создание пользовательского метода проверки подлинности для AD FS в Windows Server 2012 R2](https://go.microsoft.com/fwlink/?LinkID=511980).

## <a name="see-also"></a>См. также:
[Управление рисками для уязвимых приложений с помощью дополнительной многофакторной аутентификации](Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
