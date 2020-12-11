---
description: 'Дополнительные сведения: Ошибка репликации 1396 ошибка входа в систему имя целевой учетной записи указано неверно'
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: 'Ошибка репликации 1396: "Вход в систему не произведен. Конечная учетная запись указана неверно."'
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: a21d4f2a5e9772393d3e84a2adb497406c693f63
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97042592"
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>Ошибка репликации 1396: "Вход в систему не произведен. Конечная учетная запись указана неверно."

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction>
    <para>В этой статье описываются симптомы, причины и способы устранения сбоев Active Directory репликации с ошибкой Win32 1396: &quot; Ошибка входа: неправильное имя целевой учетной записи.&quot; </para>
    <list class="bullet"> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">Явление</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">Позволяет</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Resolutions">Разрешения</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>Симптомы</title>
    <content>
      <para />
      <list class="ordered">
<listItem><para>Программа DCDIAG сообщает о том, что проверка Active Directory репликации завершилась ошибкой 1396: Ошибка входа в систему: неверное имя целевой учетной записи.&quot;</para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN.EXE сообщает о том, что последняя попытка репликации завершилась ошибкой с состоянием 1396.</para><para>Команды REPADMIN, которые обычно упоминают состояние 1396, включают, но не ограничиваются:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/ADD</para></listItem><listItem><para>REPADMIN/РЕПЛСУМ</para></listItem><listItem><para>REPADMIN/РЕХОСТ</para></listItem><listItem><para>REPADMIN/ШОВВЕКТОР/ЛАТЕНЦИ</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/ШОВРЕПЛ</para></listItem><listItem><para>REPADMIN/СИНКАЛЛ</para></listItem></list></TD></tr></tbody></table><para>Пример выходных данных для команды &quot; repadmin/showreps, &quot; описывающей входящую репликацию с Contoso-DC2 на Contoso-DC1, завершилась с ошибкой &quot; входа: неверное имя целевой учетной записи. &quot; ошибка показана ниже::</para><code>Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ &lt;date&gt; &lt;time&gt; failed, <codeFeaturedElement>result 1396 (0x574):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
&lt;#&gt; consecutive failure(s).
Last success @ &lt;date&gt; &lt;time&gt;.
</code></listItem><listItem><para>Команда " <ui>Реплицировать сейчас</ui> " в Active Directory "сайты и службы" возвращает значение &quot; "Ошибка входа": неправильное имя целевой учетной записи.&quot;</para><para>Если щелкнуть правой кнопкой мыши объект подключения из исходного контроллера домена и выбрать пункт <ui>репликация</ui> завершается сбоем с ошибкой &quot; входа в систему, то имя целевой учетной записи неверно. &quot; Ниже показано сообщение об ошибке на экране.</para><para>Текст заголовка диалогового окна:</para><para>Реплицировать сейчас</para><para>Текст сообщения диалогового окна: </para><para>Произошла следующая ошибка при попытке синхронизации &lt; пути DNS раздела контекста именования &gt; от исходного контроллера домена &lt; к целевому контроллеру домена &gt; &lt; &gt; : Ошибка входа: неправильное имя целевой учетной записи. Эта операция не будет продолжена. </para></listItem><listItem><para>События NTDS KCC, NTDS General или Microsoft-Windows-ActiveDirectory_DomainService с состоянием 1396 регистрируются в журнале служб каталогов в Просмотр событий.</para><para>Active Directory события, которые обычно упоминают состояние 1396, включают в себя не только:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>Идентификатор события</para></TD><TD><para>Источник события</para></TD><TD><para>Строка события</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Мастер установки доменных служб Active Directory (Dcpromo) не удалось установить подключение к следующему контроллеру домена.</para></TD></tr><tr><TD><para>1645</para><para>В этом событии выводится имя субъекта-службы из трех частей.</para></TD><TD><para>Репликация NTDS</para></TD><TD><para>Active Directory не удалось выполнить проверенный удаленный вызов процедуры на другом контроллере домена, поскольку имя участника требуемой службы для конечного контроллера домена не зарегистрировано на контроллере домена, являющемся центром распространения ключей и разрешающим данное имя участника-службы.</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Домен Active Directory служб попытались связаться со следующим глобальным каталогом, и попытки были неудачными.</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Средство проверки согласованности знаний находило подключение репликации для локальной службы каталогов только для чтения и попыталось обновить ее удаленно на следующем экземпляре службы каталогов. Операция не удалась. Будет выполнена повторная попытка.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>Сбой при попытке установить канал репликации для следующего изменяемого раздела каталога.</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS KCC</para></TD><TD><para>Попытка установить связь репликации с разделом каталога только для чтения со следующими параметрами завершилась ошибкой.</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>СЛУЖБЕ</para></TD><TD><para> Серверу не удается зарегистрировать свое имя в DNS.</para></TD></tr></tbody></table></listItem><listItem><para>Сбой DCPROMO с ошибкой на экране</para><para>Текст заголовка диалогового окна:</para><para>Сбой установки Active Directory</para><para>Текст сообщения диалогового окна:</para><para>Операция завершилась сбоем, так как службе каталогов не удалось создать объект сервера для CN = NTDS Settings, CN = Сервербеингпромотед, CN = Servers, CN = site, CN = Sites, CN = Configuration, DC = contoso, DC = com на сервере ReplicationSourceDC.contoso.com. </para><para>Убедитесь, что предоставленные сетевые учетные данные имеют достаточный доступ для добавления реплики. </para><para>
&quot;Ошибка входа в систему: неверное имя целевой учетной записи. &quot;</para><para>В этом случае события с ИДЕНТИФИКАТОРом 1645, 1168 и 1125 регистрируются на сервере, на котором выполняется повышение уровня.</para></listItem><listItem><para>Сопоставьте диск с помощью команды <embeddedLabel>net use</embeddedLabel>:</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>В этом случае сервер также может регистрировать событие с ИДЕНТИФИКАТОРом 333 в журнале системных событий и использовать большой объем виртуальной памяти для приложения, например SQL Server.</para></listItem><listItem><para>Неверное время контроллера домена.</para></listItem><listItem><para>После восстановления учетной записи KRBTGT для RODC, которая была удалена, KDC не будет запускаться на контроллере домена только для чтения. Например, после восстановления появляется ошибка 1396. </para><para>
Событие с ИД 1645 регистрируется на RODC. </para><para>
Dcdiag также сообщает об ошибке, которая не может обновить учетную запись krbtgt для RODC. </para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <title>Причины</title>
    <content>
      <para />
      <list class="ordered">
        <listItem>
          <para>Имя субъекта-службы не существует в глобальном каталоге, поиск которого выполняется в KDC от имени клиента, пытающегося пройти проверку подлинности с помощью Kerberos.</para>
          <para>В контексте Active Directory репликации клиент Kerberos является целевым контроллером домена, а KDC, выполняющий поиск имени участника-службы, скорее всего, является контроллером домена назначения, но может быть удаленным контроллером домена.</para>
        </listItem>
        <listItem>
          <para>Учетная запись пользователя или службы, которая должна содержать искомое имя субъекта-службы, не существует в глобальном каталоге, который ищет KDC от имени целевого контроллера домена, пытающегося выполнить репликацию.</para>
          <para>В контексте Active Directory репликации учетная запись исходного контроллера домена не существует в глобальном каталоге, поиск которого осуществляется КОНТРОЛЛЕРом домена от имени целевого контроллера домена, выполняющего входящую репликацию.</para>
        </listItem>
        <listItem>
          <para>Конечный контроллер домена не имеет секрета LSA для исходного домена DC.</para>
        </listItem>
        <listItem>
          <para>Искомое имя субъекта-службы существует на компьютере, отличном от учетной записи исходного контроллера домена.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>Способы устранения</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>Проверьте журнал событий службы каталогов на целевом контроллере домена для события репликации NTDS 1645 и обратите внимание на следующее:</para>
          <para>Имя целевого контроллера домена</para>
          <para>Искомое имя участника-службы ( &lt; идентификатор GUID E3514235-4B06-11D1-AB04-00C04FC2DCD2/Object для исходного контроллера домена Параметры NTDS &gt; / &lt; целевого домена объект &amp; amp; gt;. &amp; amp; lt; TLD &amp; amp; gt; @ &lt; конечный домен &gt; . &lt; доменов&gt;</para>
          <para>KDC, используемый целевым контроллером домена</para>
        </listItem>
        <listItem>
          <para>В консоли KDC, идентифицированной на шаге 1, введите: </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>Выполните проверку локатора NLTEST сразу после попытки репликации, которая завершается ошибкой 1396 на целевом контроллере домена. </para>
          <para>Это должно указывать, что сборщик ключей (KDC) выполняет поиск имен участников-служб. </para>
          <para>Сборка мусора, поиск которой выполняется в KDC, также может быть захвачена в Microsoft-Windows-ActiveDirectory_DomainService событии 1655.</para>
        </listItem>
        <listItem>
          <para>Найдите имя участника-службы, обнаруженное на шаге 1, в глобальном каталоге, обнаруженном на шаге 2.</para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:&quot;(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)&quot; /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>ИЛИ</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter &quot;(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)&quot; -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>Убедитесь, что объект узла для имени субъекта-службы существует.</para>
          <para>Проверьте путь различающегося имени для объекта узла, в том числе от того, является ли объект CNF, конфликтным или размещенным в контейнере "Потерянные и найденные".</para>
          <para>Убедитесь, что исходный контроллер домена Active Directory SPN репликации зарегистрирован только в учетной записи исходного компьютера DC.</para>
          <para>Если имя субъекта-службы репликации отсутствует, убедитесь, что исходный контроллер домена зарегистрировал свое имя участника-службы, а также в том, отсутствует ли имя SPN в GC, используемом KDC, в связи с простой задержкой репликации или сбоем репликации.</para>
        </listItem>
        <listItem>
          <para>Проверьте работоспособность безопасного канала и работоспособность доверия.</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>Устранение неполадок Active Directory операций, которые завершились ошибкой 1396: Ошибка входа в систему: неверное имя целевой учетной записи.</linkText>
      <linkUri><a href="https://support.microsoft.com/kb/2183411/en-gb" data-raw-source="https://support.microsoft.com/kb/2183411/en-gb">https://support.microsoft.com/kb/2183411/en-gb</a></linkUri>
    </externalLink>
  </relatedTopics>
</developerConceptualDocument>


