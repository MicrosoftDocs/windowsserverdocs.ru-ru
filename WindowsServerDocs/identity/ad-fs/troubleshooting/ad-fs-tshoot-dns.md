---
title: Устранение неполадок AD FS. разрешение DNS
description: В этом документе описывается, как устранять неполадки в DNS-аспектах AD FS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.openlocfilehash: b0134478ce0a4e91d6e33d5a0845a2be5df53d3f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954180"
---
# <a name="ad-fs-troubleshooting---dns"></a>Устранение неполадок AD FS — DNS
Одно из первых проверок, если AD FS не работает или не отвечает, является разрешением DNS-имен.  Это базовые тесты, позволяющие определить, находятся ли AD FS серверы или серверы WAP в сети.  Для внутренних пользователей эти тесты должны разрешаться на AD FS серверы (STS).    Для внешних пользователей эти тесты должны разрешаться на серверы WAP.

В оставшейся части этого документа будет показано, как выполнять некоторые проверки быстрого разрешения имен с помощью программ командной строки.

## <a name="ping-test"></a>Проверка связи
Проверяет подключение на уровне IP к другому компьютеру TCP/IP, отправляя сообщения эхо-запросов протокола ICMP. Отображаются сообщения о получении соответствующих эхо-ответов, а также время кругового пути.  Дополнительные сведения см. в разделе [Проверка связи](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff961503(v=ws.11)).


>[!NOTE]
>Имейте в виду, что некоторые организации блокируют этот порт на своих серверах, и вы можете получить ответ **время ожидания запроса** .

### <a name="to-use-a-ping-test"></a>Использование проверки связи
1.  Откройте окно командной строки.
2. Введите команду PING <name of adfs server> a. Пример: PING sts.contoso.com
3. Вы должны увидеть ответ от сервера

![Проверка связи](media/ad-fs-tshoot-dns/dns1.png)

## <a name="nslookup"></a>Программы
Отображает сведения, которые можно использовать для диагностики инфраструктуры системы доменных имен (DNS).  Дополнительные сведения см. в разделе [nslookup](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc725991(v=ws.11)).

### <a name="to-use-a-nslookup"></a>Использование NSLookup
1.  Откройте окно командной строки.
2. Введите команду PING <name of adfs server> a. Пример: nslookup sts.contoso.com
3. Вы должны увидеть сведения о DNS для сервера ![ nslookup.](media/ad-fs-tshoot-dns/dns2.png)

## <a name="tracert"></a>Tracert
Определяет путь, полученный к назначению путем отправки эхо-запроса протокола ICMP или ICMPv6-сообщений в назначение с добавочным увеличением срока жизни (TTL) значений полей.   Дополнительные сведения см. в разделе [tracert](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff961507(v=ws.11)).


### <a name="to-use-tracert"></a>Использование tracert
1.  Откройте окно командной строки.
2. Введите tracert <name of adfs server> a. Пример: tracert sts.contoso.com
3. Должен отобразиться целевой путь, используемый для доступа к tracert сервера. ![](media/ad-fs-tshoot-dns/dns3.png)

## <a name="next-steps"></a>Next Steps

- [Устранение неполадок в AD FS](ad-fs-tshoot-overview.md)
