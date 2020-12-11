---
description: 'Дополнительные сведения: ИД события 2088: Ошибка уточняющего запроса DNS при репликации'
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: ИД события 2088 — Ошибка уточняющего запроса DNS при репликации
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: cb0a75c7573c25441fc38d761a866789fe5a1c33
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049602"
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>Событие c идентификатором 2088: сбой поиска в DNS при успешной репликации

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Когда конечный контроллер домена с Windows Server 2003 с пакетом обновления 1 (SP1) получает событие с ИДЕНТИФИКАТОРом 2088 в журнале событий службы каталогов, пытается разрешить глобальный уникальный идентификатор (GUID) в записи ресурса псевдонима (CNAME) в IP-адрес исходного контроллера домена. Однако конечный контроллер домена попытался разрешить имя и выполнить его, используя полное доменное имя (FQDN) или NetBIOS-имя исходного контроллера домена. Хотя репликация прошла успешно, проблему с системой доменных имен (DNS) следует диагностировать и устранить.

Ниже приведен пример текста события.

```
Log Name: Directory Service
Source: Microsoft-Windows-ActiveDirectory_DomainService
Date: 3/15/2008  9:20:11 AM
Event ID: 2088
Task Category: DS RPC Client
Level: Warning
Keywords: Classic
User: ANONYMOUS LOGON
Computer: DC3.contoso.com
Description:
Active Directory could not use DNS to resolve the IP address of the source domain controller listed below. To maintain the consistency of Security groups, group policy, users and computers and their passwords, Active Directory Domain Services successfully replicated using the NetBIOS or fully qualified computer name of the source domain controller.
```

Недействительная конфигурация DNS может влиять на другие базовые операции на компьютерах-членах, контроллерах домена или серверах приложений в этом лесу домен Active Directory Services, включая проверку подлинности входа или доступ к сетевым ресурсам.

Следует немедленно устранить эту ошибку конфигурации DNS, чтобы этот контроллер домена мог разрешить IP-адрес исходного контроллера домена с помощью DNS.

Альтернативное имя сервера: DC1 не удалось выполнить DNS-имя узла: 4a8717eb-8e58-456c-995a-c92e4add7e8e._msdcs. contoso. com

Примечание. по умолчанию для любого 12-часового периода отображается не более 10 ошибок DNS, даже если происходит более 10 сбоев.  Чтобы регистрировать все индивидуальные события сбоя, задайте для следующего параметра реестра диагностики значение 1:

Путь реестра: клиент RPC HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS

Действие пользователя:

1) Если исходный контроллер домена больше не работает или его операционная система переустановлена с другим именем компьютера или GUID объекта НТДСДСА, удалите метаданные исходного контроллера домена с ntdsutil.exe, выполнив действия, описанные в статье МСКБ 216498.

2) Убедитесь, что исходный контроллер домена работает Active Directory и доступен в сети, введя "NET View \\ <source DC name> " или "ping <source DC name> ".

3) Убедитесь, что исходный контроллер домена использует допустимый DNS-сервер для служб DNS и что запись узла и запись CNAME исходного контроллера домена зарегистрированы правильно, используя улучшенную версию службы DNS DCDIAG.EXE, доступную на <https://www.microsoft.com/dns>

Dcdiag/test: DNS

4) Убедитесь, что этот конечный контроллер домена использует допустимый DNS-сервер для служб DNS, запустив расширенную версию службы DNS DCDIAG.EXE в консоли конечного контроллера домена следующим образом:

Dcdiag/test: DNS

5) Дальнейший анализ ошибок DNS см. в статье KB 824449: <https://support.microsoft.com/?kbid=824449>

Дополнительное значение ошибки данных: 11004 запрошенное имя допустимо, но данные запрошенного типа не найдены </code></introduction>
  <section>
    <title>Diagnosis</title>
    <content>
      <para>Сбой разрешения имени исходного контроллера домена с помощью записи ресурса псевдонима (CNAME) в DNS может быть вызвана невозможностью настройки DNS или задержками при распространении данных DNS.</para>
    </content>
  </section>
  <section>
    <title>Решение</title>
    <content>
      <para>Выполните тестирование DNS, как описано в &quot; <link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">событии с идентификатором 2087: сбой уточняющего запроса DNS привел к сбою репликации</link>.&quot;</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>
