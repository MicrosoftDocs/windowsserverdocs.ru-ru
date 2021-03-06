---
description: 'Дополнительные сведения: использование утверждений AD DS с AD FS'
ms.assetid: 460792e4-9f1d-4e7b-b6b2-53e057f839df
title: Использование утверждений AD DS в AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 3220d171bfb54a249da1e444d48b2462019650b8
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049962"
---
# <a name="using-ad-ds-claims-with-ad-fs"></a>Использование утверждений AD DS в AD FS


Вы можете включить более широкие возможности управления доступом для федеративных приложений с помощью домен Active Directory Services \( AD DS \) \- выданных утверждений пользователей и устройств вместе с службы федерации Active Directory (AD FS) \( AD FS \) .

## <a name="about-dynamic-access-control"></a>О динамическом контроле доступа
В Windows Server &reg; 2012 функция динамического контроля доступа позволяет организациям предоставлять доступ к файлам на основе утверждений пользователей, использующих \( атрибуты учетной записи пользователя \) и заявки на устройства, \( источником которых являются атрибуты учетной записи компьютера \) , выданные службами домен Active Directory Services \( AD DS \) . AD DS выданные утверждения интегрированы в встроенную проверку подлинности Windows через протокол проверки подлинности Kerberos.

Дополнительные сведения о динамическом контроле доступа см. в разделе [Динамическая схема управления содержимым](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP).

### <a name="whats-new-in-ad-fs"></a>Новые возможности AD FS
В качестве расширения для сценария динамического контроля доступа AD FS в Windows Server 2012 теперь можно:

-   Доступ к атрибутам учетной записи компьютера в дополнение к атрибутам учетной записи пользователя в AD DS. В предыдущих версиях AD FS служба федерации не удалось получить доступ к атрибутам учетной записи компьютера с AD DS.

-   Использование AD DS выданных утверждений пользователей или устройств, которые находятся в билете проверки подлинности Kerberos. В предыдущих версиях AD FS механизму утверждений удалось прочитать идентификаторы безопасности SID пользователя и группы \( \) из Kerberos, но ему не удалось прочитать сведения о заявках, содержащиеся в билете Kerberos.

-   Преобразование AD DS выданных утверждений пользователя или устройства в токены SAML, которые могут использоваться приложениями для выполнения расширенного контроля доступа.

## <a name="benefits-of-using-ad-ds-claims-with-ad-fs"></a>Преимущества использования AD DS утверждений с AD FS
Эти AD DS выданные утверждения можно вставить в билеты проверки подлинности Kerberos и использовать с AD FS для предоставления следующих преимуществ.

-   Организации, которым требуются более широкие политики управления доступом, могут обеспечить \- доступ на основе утверждений к приложениям и ресурсам с помощью AD DS выданных утверждений, основанных на значениях атрибутов, хранящихся в AD DS для данной учетной записи пользователя или компьютера. Это помогает администраторам сократить дополнительные издержки, связанные с созданием и управлением:

    -   AD DS группы безопасности, которые в противном случае использовались для управления доступом к приложениям и ресурсам, доступным через встроенную проверку подлинности Windows.

    -   Доверия лесов, которые в противном случае использовались для управления доступом \- к \- \( \) \/ приложениям и ресурсам, доступным для бизнеса и бизнес B2B.

-   Теперь организации могут предотвратить несанкционированный доступ к сетевым ресурсам с клиентских компьютеров в зависимости от того, хранится ли значение атрибута учетной записи компьютера в AD DS например \( , DNS-имя компьютера \) соответствует политике управления доступом ресурса \( , например, файлового сервера, аклд с утверждениями \) или политикой проверяющей стороны \( , например, \- веб-приложение, поддерживающее утверждения \) . Это поможет администраторам настроить более тонкую политику контроля доступа для ресурсов или приложений, которые:

    -   Доступно только через встроенную проверку подлинности Windows.

    -   Доступ через Интернет через AD FS механизмы проверки подлинности. AD FS можно использовать для преобразования AD DS выданных утверждений устройства в утверждения AD FS, которые могут быть инкапсулированы в маркеры SAML, которые могут использоваться в ресурсе, доступном для Интернета или приложении проверяющей стороны.

## <a name="differences-between-ad-ds-and-ad-fs-issued-claims"></a>Различия между AD DS и AD FS выдано утверждений
Есть два отличительных фактора, которые важны для понимания заявок, выдаваемых из AD DS и AD FS. Эти отличия описаны ниже.

-   AD DS может выдавать только утверждения, инкапсулированные в билеты Kerberos, а не токены SAML. Дополнительные сведения о том, как AD DS выдает заявки, см. в разделе [динамический контроль доступа к содержимому](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP).

-   AD FS может выдавать только утверждения, инкапсулированные в токенах SAML, а не билеты Kerberos. Дополнительные сведения о том, как AD FS выдает утверждения, см. [в разделе роль подсистемы утверждений](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md).

## <a name="how-ad-ds-issued-claims-work-with-ad-fs"></a>Использование утверждений, выданных доменными службами Active Directory, в службах федерации Active Directory
AD DS выданные утверждения могут использоваться с AD FS для доступа к утверждениям пользователей и устройств непосредственно из контекста проверки подлинности пользователя, а не для создания отдельного вызова LDAP к Active Directory. На следующем рисунке и соответствующих шагах описывается, как этот процесс работает более подробно, чтобы обеспечить \- Управление доступом на основе утверждений для сценария динамического управления доступом.

![использование утверждений](media/UsingADDSClaimswithADFS.gif)

1.  Администратор AD DS использует консоль центр администрирования Active Directory или командлеты PowerShell для включения конкретных объектов типа утверждения в схеме AD DS.

2.  Администратор AD FS использует консоль управления AD FS для создания и настройки отношений доверия с поставщиком утверждений и проверяющей стороной с помощью \- правил утверждения или преобразования.

3.  Клиент Windows пытается получить доступ к сети. В рамках процесса проверки подлинности Kerberos клиент предоставляет билет TGT билета пользователя и компьютера, \- \( \) который еще не содержит никаких утверждений, на контроллер домена. Затем контроллер домена ищет в AD DS включенные типы утверждений и включает все полученные утверждения в возвращенный билет Kerberos.

4.  Когда клиент пользователя \/ пытается получить доступ к файловому ресурсу, аклд запрос на получение утверждений, он может получить доступ к ресурсу, так как составной идентификатор, полученный от Kerberos, имеет эти утверждения.

5.  Когда тот же клиент пытается получить доступ к веб-сайту или веб-приложению, настроенному для проверки подлинности AD FS, пользователь перенаправляется на AD FS сервер федерации, настроенный для встроенной проверки подлинности Windows. Клиент отправляет запрос контроллеру домена по протоколу Kerberos. Контроллер домена выдает билет Kerberos, содержащий запрошенные заявки, которые клиент может предоставить серверу федерации.

6.  В зависимости от способа настройки правил утверждений для поставщика утверждений и отношений доверия проверяющей стороны, настроенного ранее администратором, AD FS считывает утверждения из билета Kerberos и включает их в токен SAML, который выдается клиенту.

7.  Клиент получает маркер SAML, содержащий правильные утверждения, а затем перенаправляет его на веб-сайт.

Дополнительные сведения о создании правил утверждений, необходимых для AD DS выданных утверждений для работы с AD FS, см. в разделе [Создание правила для преобразования входящего утверждения](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md).

## <a name="see-also"></a>См. также:
[Руководство по разработке служб федерации Active Directory в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
