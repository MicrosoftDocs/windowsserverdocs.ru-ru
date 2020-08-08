---
title: NTLM Overview
description: Безопасность Windows Server
ms.topic: article
ms.assetid: 773909fd-c0bc-498a-95fc-bb452ec04d90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 4a86b2571ab586bf2289ba263346a791ea28b02e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943884"
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

Для того чтобы сократить использование протокола NTLM в ИТ-среде, необходимо знать требования развернутых в NTLM приложений, а также стратегии и шаги, необходимые для настройки вычислительных сред, использующих другие протоколы. Добавлены новые инструменты и параметры, которые помогут вам понять принципы использования NTLM и выборочно ограничить трафик NTLM. Сведения о том, как анализировать и ограничивать использование NTLM в своих средах, см. в разделе [Вводные сведения об ограничении аутентификации NTLM](https://technet.microsoft.com/library/dd560653(v=ws.10).aspx) (руководство по аудиту и ограничению использования NTLM).

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
|**Оценка продукта**|[Вводные сведения об ограничении аутентификации NTLM](https://technet.microsoft.com/library/dd560653.aspx)<p>[Изменения в аутентификации NTLM](https://technet.microsoft.com/library/dd566199.aspx)|
|**Planning**|[Руководство по моделированию угроз в ИТ-инфраструктуре](https://technet.microsoft.com/library/dd941826.aspx)<p>[Угрозы и меры противодействия: Параметры безопасности в Windows Server 2003 и Windows XP](https://technet.microsoft.com/library/dd162275.aspx)<p>[Руководство по угрозам и мерам противодействия: Параметры безопасности в Windows Server 2008 и Windows Vista](https://technet.microsoft.com/library/dd349791.aspx)<p>[Руководство по угрозам и мерам противодействия. Параметры безопасности в Windows Server 2008 R2 и Windows 7](https://technet.microsoft.com/library/hh125921.aspx)|
|**Развертывание**|[Расширенная защита для проверки подлинности](https://support.microsoft.com/kb/968389)<p>[Руководство по аудиту и ограничению использования NTLM](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)<p>[Задайте вопрос в блоге команды разработчиков служб каталогов: Блокировка NTLM и вы: Методики анализа приложений и аудита в Windows 7](https://blogs.technet.com/askds/archive/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7.aspx)<p>[Блог, посвященный аутентификации Windows](https://blogs.technet.com/authentication/)<p>[Настройка MaxConcurrentAPI для сквозной аутентификации NTLM](https://support.microsoft.com/help/2688798/how-to-do-performance-tuning-for-ntlm-authentication-by-using-the-maxc)|
|**Разработка**|[Windows NTLM (Microsoft) \(\)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)<p>[\[MS \- нлмп \] : \( \) Спецификация протокола проверки подлинности NTLM диспетчера LAN Manager](https://msdn.microsoft.com/library/cc236621(PROT.10).aspx)<p>[\[MS \- NNTP \] : \( \) Проверка подлинности NTLM диспетчера LAN Manager: \( расширение NNTP для протокола сетевого обмена \)](https://msdn.microsoft.com/library/cc236774(PROT.10).aspx)<p>[\[MS \- НСТ \] : Спецификация протокола NTLM по ПРОТОКОЛу HTTP](https://msdn.microsoft.com/library/cc237488(PROT.10).aspx)|
|**Устранение неполадок**|Пока недоступно|
|**Ресурсы сообщества**|[И снова о том же: "узкие места" NTLM и среда выполнения RPC](https://blogs.technet.com/b/askds/archive/2011/09/15/is-this-horse-dead-yet-ntlm-bottlenecks-and-the-rpc-runtime.aspx)|



