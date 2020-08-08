---
title: AD FS устранение неполадок — Fiddler-WS-Federation
description: В этом документе приведена детальная трассировка сервера WS-Federation Exchange с AD FS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/18/2018
ms.topic: article
ms.openlocfilehash: f30b66bd80b3c5002bdc2c66a1d89718cdb1ee39
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956211"
---
# <a name="ad-fs-troubleshooting---fiddler---ws-federation"></a>AD FS устранение неполадок — Fiddler-WS-Federation

![Схема федерации AD FS и Windows Server](media/ad-fs-tshoot-fiddler-ws-fed/fiddler9.png)

## <a name="step-1-and-2"></a>Шаг 1 и 2

Это начало нашей трассировки.  В этом фрейме отображаются следующие сведения:

![Начало трассировки Fiddler](media/ad-fs-tshoot-fiddler-ws-fed/fiddler1.png)

Запрос:

- HTTP-получение для нашей проверяющей стороны (http://sql1.contoso.com/SampApp)

Ответ:

- Ответом является HTTP 302 (Redirect).  Данные транспорта в заголовке ответа показывают, куда перенаправляться (https://sts.contoso.com/adfs/ls)
- URL-адрес перенаправления содержит WA = wsignin 1,0, который сообщает нам, что наше приложение RP создало запрос на вход WS-Federation для нас и отправило его в конечную точку/адфс/ЛС/AD FS.  Это называется привязкой перенаправления.

![Передача данных в заголовке ответа](media/ad-fs-tshoot-fiddler-ws-fed/fiddler2.png)

## <a name="step-3-and-4"></a>Шаг 3 и 4

![Трассировка Fiddler продолжения](media/ad-fs-tshoot-fiddler-ws-fed/fiddler3.png)

Запрос:

- HTTP-получение к серверу AD FS (STS. contoso. com)

Ответ:

- Ответ — запрос учетных данных.  Это означает, что мы используем Forms ауснетикатион
- Щелкнув WebView ответа, можно увидеть запрос учетных данных.

![Продолжение трассировки Fiddler](media/ad-fs-tshoot-fiddler-ws-fed/fiddler6.png)

## <a name="step-5-and-6"></a>Шаг 5 и 6

![Вкладка WebView экрана запроса учетных данных](media/ad-fs-tshoot-fiddler-ws-fed/fiddler4.png)

Запрос:

- HTTP POST с нашим именем пользователя и паролем.
- Мы представим свои учетные данные.  Просмотрев необработанные данные в запросе, можно увидеть учетные данные

Ответ:

- Ответ найден, и создается и возвращается зашифрованный файл cookie Мсиаус.  Используется для проверки утверждения SAML, созданного нашим клиентом.  Это также называется "cookie для проверки подлинности" и будет присутствовать только в том случае, если AD FS является IDP.

## <a name="step-7-and-8"></a>Шаг 7 и 8

![Продолжение трассировки Fiddler](media/ad-fs-tshoot-fiddler-ws-fed/fiddler5.png)

Запрос:

- Теперь, когда мы прошли проверку подлинности, мы выполняем еще один HTTP-запрос на сервер AD FS и представлю маркер проверки подлинности.

Ответ:

- Ответом является HTTP OK, что означает, что AD FS прошел проверку подлинности пользователя на основе предоставленных учетных данных.
- Кроме того, мы устанавливаем значение 3 файлов cookie обратно клиенту.
    - Мсисаусентикатед содержит значение метки времени в кодировке Base64 для, когда клиент прошел проверку подлинности.
    - Мсислупдетектионкукие используется механизмом обнаружения бесконечного цикла AD FS для остановки клиентов, которые завершились в бесконечном цикле перенаправления на сервере федерации. Данные файла cookie представляют собой отметку времени в кодировке Base64.
    - Мсиссигнаут используется для наблюдения за IdP и всеми RP, посещаемыми для сеанса единого входа. Этот файл cookie используется при вызове выхода WS-Federation. Содержимое этого файла cookie можно просмотреть с помощью декодера Base64.

## <a name="step-9-and-10"></a>Шаг 9 и 10

![Продолжение трассировки Fiddler](media/ad-fs-tshoot-fiddler-ws-fed/fiddler7.png)

Запрос:

- HTTP POST

Ответ:

- Ответ найден

## <a name="step-11-and-12"></a>Шаг 11 и 12

![Завершение трассировки Fiddler](media/ad-fs-tshoot-fiddler-ws-fed/fiddler8.png)

Запрос:

- ПОЛУЧЕНИЕ HTTP

Ответ:

- Ответ — ОК.

## <a name="next-steps"></a>Next Steps

- [Устранение неполадок в AD FS](ad-fs-tshoot-overview.md)