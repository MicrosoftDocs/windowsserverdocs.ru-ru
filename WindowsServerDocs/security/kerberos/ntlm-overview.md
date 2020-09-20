---
title: NTLM Overview
description: Безопасность Windows Server
ms.topic: article
ms.assetid: 773909fd-c0bc-498a-95fc-bb452ec04d90
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: d12e61fac3ba6c44dbcac35ea3097e95db54752a
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766787"
---
# <a name="ntlm-overview"></a>NTLM Overview

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

В этой статье для ИТ Professional описывается NTLM, любые изменения в работе и предоставляются ссылки на технические ресурсы по проверке подлинности Windows и NTLM для Windows Server 2012 и предыдущих версий.

## <a name="feature-description"></a><a name="BKMK_OVER"></a>Описание функции
Проверка подлинности NTLM — это семейство протоколов проверки подлинности, которые входят в0.dll Windows Msv1 \_ . Протоколы проверки подлинности NTLM включают LAN Manager версий 1 и 2, а также NTLM версий 1 и 2. Протоколы проверки подлинности NTLM выполняют проверку подлинности пользователей и компьютеров на основе \/ механизма реагирования на запрос, который доказывает серверу или контроллеру домена о том, что пользователь знает пароль, связанный с учетной записью. При использовании протокола NTLM сервер ресурсов должен выполнять одно из следующих действий для проверки удостоверения пользователя или компьютера каждый раз, как возникает необходимость в новом маркере доступа:

-   Свяжитесь со службой проверки подлинности домена на контроллере домена, чтобы получить домен учетной записи компьютера или пользователя, если эта учетная запись является учетной записью в домене.

-   Если же учетная запись пользователя или компьютера является локальной учетной записью, то ее можно найти в локальной базе данных учетных записей.

## <a name="current-applications"></a><a name="BKMK_APP"></a>Текущие приложения
Аутентификация NTLM по-прежнему поддерживается и обязательна для использования при выполнении аутентификации Windows с системами, настроенными как элемент рабочей группы. Проверка подлинности NTLM также используется для проверки подлинности локального входа на \- контроллеры, не являющиеся доменами. Проверка подлинности Kerberos версии 5 является предпочтительным методом проверки подлинности для Active Directoryных сред, но приложение, не \- использующее Майкрософт или Microsoft, может по-прежнему использовать NTLM.

Для того чтобы сократить использование протокола NTLM в ИТ-среде, необходимо знать требования развернутых в NTLM приложений, а также стратегии и шаги, необходимые для настройки вычислительных сред, использующих другие протоколы. Добавлены новые инструменты и параметры, которые помогут вам понять принципы использования NTLM и выборочно ограничить трафик NTLM. Сведения о том, как анализировать и ограничивать использование NTLM в своих средах, см. в разделе [Вводные сведения об ограничении аутентификации NTLM](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560653(v=ws.10)) (руководство по аудиту и ограничению использования NTLM).

## <a name="new-and-changed-functionality"></a><a name="BKMK_NEW"></a>Новые и измененные функции
Нет изменений в функциональности NTLM для Windows Server 2012.

## <a name="removed-or-deprecated-functionality"></a><a name="BKMK_DEP"></a>Удаленные или устаревшие функциональные возможности
Отсутствует удаленная или устаревшая функциональность для NTLM для Windows Server 2012.

## <a name="server-manager-information"></a><a name="BKMK_INSTALL"></a>Сведения о диспетчере сервера
NTLM нельзя использовать с диспетчером серверов. Для управления использованием проверки подлинности NTLM между компьютерными системами можно использовать параметры политики безопасности или групповые политики. В доменах протоколом проверки по умолчанию является Kerberos.

## <a name="see-also"></a><a name="BKMK_LINKS"></a> См. также
В следующей таблице представлены материалы по NTLM и другим технологиям проверки подлинности Windows.

|Тип содержимого|Ссылки|
|--------|-------|
|**Оценка продукта**|[Вводные сведения об ограничении аутентификации NTLM](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560653(v=ws.10))<p>[Изменения в аутентификации NTLM](/previous-versions/windows/it-pro/windows-7/dd566199(v=ws.10))|
|**Planning**|[Руководство по моделированию угроз в ИТ-инфраструктуре](/previous-versions/tn-archive/dd941826(v=technet.10))<p>[Угрозы и меры противодействия: Параметры безопасности в Windows Server 2003 и Windows XP](/previous-versions/tn-archive/dd162275(v=technet.10))<p>[Руководство по угрозам и мерам противодействия: Параметры безопасности в Windows Server 2008 и Windows Vista](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd349791(v=ws.10))<p>[Руководство по угрозам и мерам противодействия. Параметры безопасности в Windows Server 2008 R2 и Windows 7](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh125921(v=ws.10))|
|**Deployment**|[Расширенная защита для проверки подлинности](https://support.microsoft.com/kb/968389)<p>[Руководство по аудиту и ограничению использования NTLM](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/jj865674(v=ws.10))<p>[Задайте вопрос в блоге команды разработчиков служб каталогов: Блокировка NTLM и вы: Методики анализа приложений и аудита в Windows 7](https://blogs.technet.com/askds/archive/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7.aspx)<p>[Блог, посвященный аутентификации Windows](https://blogs.technet.com/authentication/)<p>[Настройка MaxConcurrentAPI для сквозной аутентификации NTLM](https://support.microsoft.com/help/2688798/how-to-do-performance-tuning-for-ntlm-authentication-by-using-the-maxc)|
|**Разработка**|[Windows NTLM (Microsoft) \(\)](/windows/win32/secauthn/microsoft-ntlm)<p>[\[MS \- нлмп \] : \( \) Спецификация протокола проверки подлинности NTLM диспетчера LAN Manager](/openspecs/windows_protocols/ms-nlmp/b38c36ed-2804-4868-a9ff-8dd3182128e4)<p>[\[MS \- NNTP \] : \( \) Проверка подлинности NTLM диспетчера LAN Manager: \( расширение NNTP для протокола сетевого обмена \)](/openspecs/windows_protocols/ms-nntp/73ae7d96-30fe-4750-807c-bfe7c38b3a0a)<p>[\[MS \- НСТ \] : Спецификация протокола NTLM по ПРОТОКОЛу HTTP](/openspecs/windows_protocols/ms-ntht/f09cf6e1-529e-403b-a8a5-7368ee096a6a)|
|**Устранение неполадок**|Пока недоступно|
|**Ресурсы сообщества**|[И снова о том же: "узкие места" NTLM и среда выполнения RPC](https://blogs.technet.com/b/askds/archive/2011/09/15/is-this-horse-dead-yet-ntlm-bottlenecks-and-the-rpc-runtime.aspx)|