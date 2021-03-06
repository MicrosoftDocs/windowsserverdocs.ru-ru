---
title: Шаг 1. Планирование базовой инфраструктуры DirectAccess
description: Узнайте, как выполнить планирование инфраструктуры, необходимой для базового развертывания DirectAccess.
manager: brianlic
ms.topic: article
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 3c93aa714687a2b62448e0113fca2174fff2d627
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101834295"
---
# <a name="step-1-plan-the-basic-directaccess-infrastructure"></a>Шаг 1. Планирование базовой инфраструктуры DirectAccess
Первым шагом для базового развертывания DirectAccess на одном сервере является планирование инфраструктуры, необходимой для развертывания. В этом разделе пошагово описывается планирование инфраструктуры:

|Задача|Описание|
|----|--------|
|Планирование топологии сети и настроек|Определите, где будет располагаться сервер DirectAccess (на границе либо за устройством преобразования сетевых адресов (NAT) или брандмауэром), а также спланируйте IP-адресацию и маршрутизацию.|
|Планирование требований к брандмауэру|Определите, каким образом доступ DirectAccess будет разрешаться на пограничных брандмауэрах.|
|Планирование требований к сертификатам|Для DirectAccess может использоваться Kerberos или сертификаты проверки подлинности клиентов. При развертке базового DirectAccess происходит автоматическая настройка прокси-сервера Kerberos, а для проверки подлинности используются учетные данные Active Directory.|
|Планирование требования к DNS|Определите настройки DNS для сервера DirectAccess, серверов инфраструктуры и клиентских подключений.|
|Планирование Active Directory|Определите требования к контроллерам домена и Active Directory.|
|Планирование объектов групповой политики|Определите, какие объекты групповой политики требуются вашей организации и как производить их создание и редактирование.|

Указанные задачи можно выполнять в произвольном порядке.

## <a name="plan-network-topology-and-settings"></a><a name="bkmk_1_1_Network_svr_top_settings"></a>Планирование топологии сети и настроек

### <a name="plan-network-adapters-and-ip-addressing"></a>Планирование конфигурации сетевых адаптеров и параметров IP-адресации

1.  Определите, какую топологию сетевых адаптеров хотите использовать. Для установки DirectAccess могут использоваться следующие варианты:

    -   С двумя сетевыми адаптерами — либо в пограничном месте с одним сетевым адаптером, подключенным к Интернету, либо с помощью NAT, брандмауэра или маршрутизатора, с одним сетевым адаптером, подключенным к сети периметра, а другим — к внутренней сети.

    -   За устройством NAT с одним сетевым адаптером — сервер DirectAccess устанавливается за пределами устройства NAT, а один сетевой адаптер подключается к внутренней сети.

2.  Определение требований к IP-адресации:

    Для установки безопасного подключения клиентских компьютеров к внутренней сети корпорации в технологии DirectAccess используются протоколы IPv6 и IPsec. Однако для работы DirectAccess необязательно подключаться к Интернету по IPv6 или использовать во внутренних сетях оборудование с поддержкой IPv6. Вместо этого происходит автоматическая настройка туннелирования для IPv6, чтобы работать с IPv6-трафиком в IPv4-интернете (6to4, Teredo, IP-HTTPS), а также в интрасетях, поддерживающих только IPv4 (NAT64 или ISATAP). Общие сведение об этих технологиях туннелирования см. в следующих разделах:

    -   [Технологии туннелирования IPv6](/previous-versions/bb726951(v=technet.10))

    -   [Спецификация протокола туннелирования IP-HTTPS](/previous-versions/bb726951(v=technet.10))

3.  Выполните необходимые настройки адаптеров и адресации в соответствии со следующей таблицей. Для развертываний за устройством NAT с помощью одного сетевого адаптера настройте IP-адреса, используя только столбец **внутренний сетевой адаптер** .

    |Описание|Внешний сетевой адаптер|Внутренний сетевой адаптер <sup>1</sup>|Требования к маршрутизации|
    |-|--------------|--------------------|------------|
    |IPv4-интрасеть и IPv4-интернет|Настройте следующие параметры.<p>— Один статический общедоступный IPv4-адрес с соответствующей маской подсети.<br />— IPv4-адрес шлюза по умолчанию брандмауэра Интернета или локального маршрутизатора поставщика услуг Интернета (ISP).|Настройте следующие параметры.<p>— Адрес интрасети IPv4 с соответствующей маской подсети.<br />— Зависящий от подключения DNS-суффикс пространства имен интрасети. Необходимо также настроить DNS-сервер во внутреннем интерфейсе.<br />Не настраивайте шлюз по умолчанию для всех интерфейсов интрасети.|Чтобы настроить север DirectAccess для работы со всеми подсетями внутренней IPv4-сети:<p>1. Выведите список пространств адресов IPv4 для всех расположений в интрасети.<br />2. с помощью команд **Route Add-p** или **netsh interface IPv4 добавьте команды Route** , чтобы добавить адресные пространства IPv4 в качестве статических маршрутов в таблице маршрутизации IPv4 сервера DirectAccess.|
    |IPv6-интернет и IPv6-интрасеть|Настройте следующие параметры.<p>— Используйте конфигурацию настроенного адреса, предоставленную поставщиком услуг Интернета.<br />— Используйте команду **route print** , чтобы убедиться, что маршрут IPv6 по умолчанию, указывающий на маршрутизатор поставщика услуг Интернета, существует в таблице маршрутизации IPv6.<br />— Определить, используют ли маршрутизаторы ISP и интрасети параметры маршрутизатора по умолчанию, описанные в RFC 4191, и использовать более высокий приоритет по умолчанию, чем маршрутизаторы локальной интрасети. Если эти условия выполняются, дальнейшие настройки маршрута по умолчанию не требуются. Использование большего приоритета для маршрутизатора провайдера подразумевает, что активный маршрут IPv6 по умолчанию сервера DirectAccess направлен в IPv6-интернет.<p>Поскольку сервером DirectAccess служит IPv6-маршрутизатор, при наличии собственной инфраструктуры IPv6 веб-интерфейс может также получить доступ к контроллерам домена в интрасети. В этом случае на контроллере домена в сети периметра следует использовать фильтрацию пакетов, чтобы предотвратить подключение к IPv6-адресу имеющего доступ в Интернет интерфейса сервера DirectAccess.|Настройте следующие параметры.<p>Если вы не используете уровни предпочтений по умолчанию, настройте интерфейсы интрасети с помощью команды **netsh interface IPv6 Set InterfaceIndex игноредефаултраутес = Enabled** . Эта команда позволит исключить добавление дополнительных маршрутов по умолчанию, направленных на маршрутизаторы интрасети, в таблицу маршрутизации IPv6. Вы можете узнать индекс интерфейсов вашей интрасети с помощью команды netsh interface show interface.|Если ваша интрасеть использует протокол IPv6, для настройки сервера DirectAccess и осуществления доступа ко всем расположениям IPv6 нужно выполнить следующие действия:<p>1. Выведите список пространств адресов IPv6 для всех расположений в интрасети.<br />2. с помощью команды **netsh interface IPv6 добавьте Route** , чтобы добавить адресные пространства IPv6 в качестве статических маршрутов в таблице маршрутизации IPv6 сервера DirectAccess.|
    |IPv4-Интернет и IPv6-интрасеть|Сервер DirectAccess направляет трафик маршрута IPv6 по умолчанию с помощью интерфейса адаптера Microsoft 6to4. Это позволяет осуществлять ретрансляцию 6to4 в IPv4-интернет. Вы можете настроить сервер DirectAccess на IPv4-адрес ретрансляции 6to4 в IPv4-интернет (используется, если в корпоративной сети не задействован протокол IPv6) с помощью команды netsh interface ipv6 6to4 set relay name=192.88.99.1 state=enabled command.|||

    > [!NOTE]
    > Следует отметить следующее.
    >
    > 1.  Если клиенту DirectAccess был присвоен публичный IPv4-адрес, для подключения к интрасети он будет использовать технологию туннелирования 6to4. Если клиент DirectAccess не может подключиться к серверу DirectAccess при помощи механизма 6to4, будет использован сертификат IP-HTTPS.
    > 2.  Клиентским компьютерам, поддерживающим IPv6 и подключающимся по этому протоколу к серверу DirectAccess, не требуется выполнять туннелирование.

### <a name="plan-firewall-requirements"></a><a name="ConfigFirewalls"></a>Планирование требований к брандмауэру
Если сервер DirectAccess расположен за пограничным брандмауэром и работает в IPv4-интернете, для трафика DirectAccess потребуются следующие исключения:

-   трафик 6to4 — IP-протокол 41, входящий и исходящий.

-   Протокол IP-HTTPS — порт назначения TCP 443 и порт источника TCP 443 исходящие.

-   Если вы развертываете DirectAccess с одним сетевым адаптером, а также используете сервер DirectAccess в качестве сервера сетевых расположений, TCP-порт 62000 также должен быть исключен.

    > [!NOTE]
    > Это исключение устанавливается на сервере DirectAccess. Остальные исключения устанавливаются на пограничном брандмауэре.

Если сервер DirectAccess работает в IPv6-интернете, для трафика DirectAccess потребуются следующие исключения:

-   Протокол IP 50

-   UDP-порт назначения 500 для входящих подключений и UDP-порт источника 500 для исходящих подключений.

При использовании дополнительных брандмауэров, для трафика DirectAccess необходимо установить следующие исключения во внутренней сети:

-   ISATAP — протокол 41, входящий и исходящий

-   Протоколы TCP/UDP для всех типов трафика IPv4/IPv6

### <a name="plan-certificate-requirements"></a><a name="bkmk_1_2_CAs_and_certs"></a>Планирование требований к сертификатам
Требования к сертификатам для IPsec распространяются на сертификат, используемый компьютерами клиентов DirectAccess при установке соединения IPsec и подключению к серверу DirectAccess, а также на сертификат, используемый серверами DirectAccess для установки соединения IPsec с клиентами DirectAccess. Для DirectAccess в Windows Server 2012 R2 и Windows Server 2012 использование этих сертификатов IPsec не является обязательным. Мастер начальной настройки устанавливает сервер DirectAcces в качестве прокси-сервера Kerberos, чтобы выполнять проверку подлинности IPsec без запроса сертификатов.

1.  **Сервер IP-HTTPS**. При настройке DirectAccess сервер DirectAccess автоматически назначается в качестве веб-прослушивателя IP-HTTPS. Узлу IP-HTTPS требуется сертификат веб-сайта (CRL), клиентские компьютеры должны иметь доступ к узлу со списком отзыва (CRL) для этого сертификата. Мастер установки DirectAccess пытается использовать сертификат SSTP VPN. Если SSTP не настроен, проверяется наличие сертификата для IP-HTTPS в личном хранилище устройства. Если таковой отсутствует, происходит автоматическое создание самозаверяющего сертификата.

2.  **Сервер сетевых расположений**. Сервер сетевых расположений — это веб-сайт, используемый для определения того, находятся ли клиентские компьютеры в корпоративной сети. Для сервера сетевых расположений требуется сертификат веб-сайта. Клиенты DirectAccess должны иметь доступ к сайту CRL для этого сертификата. Мастер включения удаленного доступа проверяет, есть ли в личном хранилище компьютера сертификат для сервера сетевых расположений. Если он отсутствует, автоматически создается самозаверяющий сертификат.

Требования сертификации для указанных серверов перечислены в следующей таблице:

|Проверка подлинности IPsec|Сервер IP-HTTPS|Сервер сетевого размещения|
|------------|----------|--------------|
|Внутренний ЦС необходим для выдаче сертификатов компьютеров на сервер DirectAccess и клиентов для проверки подлинности IPsec, если не используется прокси-сервер Kerberos для проверки подлинности.|Общедоступный ЦС. для выдачи сертификата IP-HTTPS рекомендуется использовать общедоступный ЦС. Это гарантирует, что точка распространения списка отзыва сертификатов будет доступна извне.|Внутренний ЦС. Вы можете использовать внутренний ЦС для выдаче сертификата веб-сайта сервера сетевого расположения. Убедитесь в абсолютной доступности точки распределения списка отзыва сертификатов из внутренней сети.|
||Внутренний ЦС. для выдаче сертификата IP-HTTPS можно использовать внутренний ЦС. Однако необходимо убедиться, что точка распространения списка отзыва сертификатов доступна извне.|Самозаверяющий сертификат. Вы можете использовать самозаверяющий сертификат для веб-сайта сервера сетевого расположения. Однако самозаверяющий сертификат нельзя использовать в многосайтовых развертываниях.|
||Самозаверяющий сертификат. Вы можете использовать самозаверяющий сертификат для сервера IP-HTTPS; Однако необходимо убедиться, что точка распространения списка отзыва сертификатов доступна извне. Самозаверяющие сертификаты неприменимы к многосайтовым развертываниям.||

#### <a name="plan-certificates-for-ip-https-and-network-location-server"></a><a name="bkmk_website_cert_IPHTTPS"></a>Планирование сертификатов для IP-HTTPS и сервера сетевых расположений
Если вы желаете предоставить соответствующий сертификат, см. раздел [Развертывание одиночного сервера DirectAccess с особыми параметрами](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md). При отсутствии сертификатов мастер начальной настройки автоматически создает соответствующие самозаверяющие сертификаты.

> [!NOTE]
> Если вы вручную предоставляете сертификаты для IP-HTTPS и сервера сетевых расположений, убедитесь, что им присваиваются имена субъектов. Если вместо имени субъекта у сертификата имеется лишь альтернативное имя, он не будет принят мастером DirectAccess.

#### <a name="plan-dns-requirements"></a>Планирование требования к DNS
Значение DNS при развертывании DirectAccess заключается в следующем:

-   **Клиентские запросы DirectAccess**. Служба DNS используется для разрешения запросов от клиентских компьютеров DirectAccess, расположенных вне внутренней сети. Клиенты DirectAccess пытаются подключиться к серверу сетевых расположений DirectAccess, чтобы определить, находятся ли они в Интернете или в корпоративной сети. Если подключение установлено успешно, клиенты будут определены в интрасети и DirectAccess не используются, а запросы клиентов разрешаются с помощью DNS-сервера, настроенного на сетевом адаптере клиентского компьютера. Если подключение не устанавливается, предполагается, что клиенты находятся в Интернете. Чтобы определить, какой DNS-сервер будет использоваться для обработки запросов имен, клиенты DirectAccess используют таблицу политики разрешения имен (NRPT). Вы можете указать, что для разрешения имен при доступе DirectAccess должен использоваться DNS64 или альтернативный внутренний DNS-сервер. При разрешении имен клиентами DirectAccess используется NRPT, чтобы определять, каким образом должен быть обработан запрос. Клиенты запрашивают полное доменное имя или одиночную метку, например http://internal . Если запрашивается однокомпонентное имя, для формирования полного доменного имени к нему добавляется DNS-суффикс. Если DNS-запрос соответствует записи в NRPT, а также указан DNS4 или DNS-сервер в интрасети, запрос на разрешение имени направляется на заданный сервер. Если есть соответствие, но DNS-сервер не указан, это указывает на правило исключения и используется обычное разрешение имен.

    Если в консоли управления DirectAccess в NRPT добавляется новый суффикс, можно выполнить автоматическое обнаружение DNS-сервера по умолчанию для этого суффикса, щелкнув кнопку **Обнаружить**. Автообнаружение работает следующим образом:

    1.  Если корпоративная сеть основана на IPv4, или же комбинации IPv4 и IPv6, адресом по умолчанию служит адрес DNS64 внутреннего адаптера сервера DirectAccess.

    2.  Если корпоративная сеть основана на IPv6, адресом по умолчанию служит IPv6-адрес DNS-серверов корпоративной сети.

> [!NOTE]
> Начиная с Windows 10 может 2020 обновление, клиент больше не регистрирует свои IP-адреса на DNS-серверах, настроенных в таблица политики разрешения имен (NRPT).
> Если требуется регистрация DNS, например " **Управление**", ее можно явно включить с помощью этого раздела реестра на клиенте:
>
> Путь: `HKLM\System\CurrentControlSet\Services\Dnscache\Parameters`<br/>
> Тип: `DWORD`<br/>
> Имя значения: `DisableNRPTForAdapterRegistration`<br/>
> Значения:<br/>
> `1` -Регистрация DNS отключена (по умолчанию, так как обновление Windows 10 может 2020)<br/>
> `0` -Регистрация DNS включена

-   **Серверы инфраструктуры**

    1.  **Сервер сетевых расположений**. Клиенты DirectAccess пытаются подключиться к серверу сетевых расположений, чтобы определить, находятся ли они во внутренней сети. Клиенты во внутренней сети должны иметь возможность разрешения имени сервера сетевых расположений. Если клиент находится во внешней сети, эта возможность должна исключаться. Для этого по умолчанию происходит добавление полного доменного имени сервера сетевых расположений в качестве правила исключения в NRPT. Кроме того, при настройке DirectAccess происходит автоматическое создание следующих правил:

        1.  Правило суффикса DNS для корневого домена или доменного имени сервера DirectAccess, а также IPv6-адресов, соответствующих DNS-серверам интрасети и настроенных на сервере DirectAccess. Например, если сервер DirectAccess server причастен к домену corp.contoso.com, создается правило для DNS-суффикса corp.contoso.com.

        2.  Правило исключения для полного доменного имени сервера сетевых расположений. Например, если URL-адрес сервера сетевого расположения — https://nls.corp.contoso.com , для полного доменного имени NLS.Corp.contoso.com создается правило исключения.

        **Сервер IP-HTTPS**. Сервер DirectAccess действует как прослушиватель IP-HTTPS и использует свой сертификат сервера для проверки подлинности клиентов IP-HTTPS. Имя IP-HTTPS должно разрешаться для клиентов DirectAccess с помощью публичных DNS-серверов.

        **Проверки подключения**. DirectAccess создает веб-пробу по умолчанию, которая используется клиентскими компьютерами DirectAccess для проверки подключения к внутренней сети. Для надлежащей работы пробы необходимо вручную зарегистрировать следующие доменные имена:

        1.  DirectAccess — вебпробехост — разрешение на внутренний IPv4-адрес сервера DirectAccess или IPv6-адрес в среде только для IPv6.

        2.  DirectAccess — корпконнективитихост — должен разрешить адрес localhost (замыкание на себя). Следует создать записи узла A (со значением 127.0.0.1) и AAAA (со значением из префикса NAT64, последние 32 бита которого заменяются значением 127.0.0.1). Префикс NAT64 можно узнать при помощи командлета get-netnattransitionconfiguration.

        Вы можете создать дополнительные средства проверки подключения, используя другие веб-адреса через HTTP или PING. Для каждого средства проверки подключения должна существовать DNS-запись.

#### <a name="dns-server-requirements"></a>Требования к DNS-серверу

-   Для клиентов DirectAccess необходимо использовать DNS-сервер под управлением Windows Server 2008, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 или любой DNS-сервер, поддерживающий IPv6.

> [!NOTE]
> При развертывании DirectAccess не рекомендуется использовать DNS-серверы под управлением Windows Server 2003 при развертывании. Хотя DNS-серверы Windows Server 2003 поддерживают записи IPv6, Windows Server 2003 больше не поддерживается корпорацией Майкрософт. Кроме того, не следует развертывать DirectAccess, если контроллеры домена работают под управлением Windows Server 2003 из-за проблемы со службой репликации файлов. Дополнительные сведения см. в разделе [Поддерживаемые конфигурации DirectAccess](../DirectAccess-Unsupported-Configurations.md).

### <a name="plan-the-network-location-server"></a><a name="bkmk_1_4_NLS"></a>Планирование сервера сетевых расположений
Сервер сетевых расположений — это веб-сайт, используемый для определения причастности клиентов DirectAccess к корпоративной сети. Клиенты, находящиеся в корпоративной сети, для доступа к внутренним ресурсам не используют DirectAccess, а подключаются напрямую.

Мастер начальной настройки автоматически настраивает сервер сетевых расположений на сервере DirectAccess и при развертывании DirectAccess происходит автоматическое создание веб-сайта. Это позволяет упростить установку, исключив использование инфраструктуры сертификатов.

Если вы хотите развернуть сервер сетевых расположений без использования самозаверяющих сертификатов, см. раздел [Развертывание одиночного сервера DirectAccess с расширенными параметрами](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).

### <a name="plan-active-directory"></a><a name="bkmk_1_6_AD"></a>Active Directory плана
DirectAccess использует Active Directory и Active Directory объекты групповой политики следующим образом:

-   **Проверка подлинности**. Active Directory используется для проверки подлинности. Для доступа к внутренним ресурсам туннель DirectAccess использует проверку подлинности Kerberos.

-   **Объекты групповой политики**. DirectAccess собирает параметры конфигурации в объекты групповой политики, которые применяются к серверам и клиентам DirectAccess.

-   **Группы безопасности**. DirectAccess использует группы безопасности, чтобы собрать вместе и идентифицировать клиентские компьютеры и серверы DirectAccess. К необходимым группам безопасности применяются групповые политики.

**Требования к Active Directory**

При планировании Active Directory для развертывания DirectAccess необходимо соблюсти следующие требования:

-   По крайней мере один контроллер домена, установленный в Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 или Windows Server 2008.

    Если контроллер домена расположен в сети периметра (и доступен для имеющего выход в Интернет сетевого адаптера сервера DirectAccess), заблокируйте доступ сервера DirectAccess к нему с помощью фильтрации пакетов, чтобы исключить подключение к IP-адресу интернет-адаптера.

-   Сервер DirectAccess должен быть членом домена.

-   Клиенты DirectAccess должны входить в состав домена. Клиенты могут принадлежать к:

    -   Любому домену в одном лесу с сервером DirectAccess.

    -   Любому домену, имеющему двустороннее доверие с доменом сервера DirectAccess.

    -   Любому домену в лесу, имеющем двустороннее доверие с лесом, к которому принадлежит домен DirectAccess.

> [!NOTE]
> - Сервер DirectAccess не может быть контроллером домена.
> - Контроллер домена Active Directory, используемый для DirectAccess, не должен быть доступен для внешнего интернет-адаптера сервера DirectAccess (адаптер не должен быть указан в доменном профиле брандмауэра Windows).

### <a name="plan-group-policy-objects"></a><a name="bkmk_1_7_GPOs"></a>Планирование объектов групповой политики
Параметры DirectAccess, настроенные при настройке DirectAccess, собираются в объекты групповой политики (GPO). Для хранения параметров DirectAccess используются следующие объекты групповой политики:

-   **Объект групповой политики клиента DirectAccess**. Этот GPO содержит параметры клиента, в том числе параметры технологии туннелирования IPv6, записи NRPT и правила безопасности подключений брандмауэра Windows в режиме повышенной безопасности. Объекты групповой политики применяются к группам безопасности, указанным для клиентских компьютеров.

-   **Объект групповой политики сервера DirectAccess**. Этот GPO содержит параметры конфигурации DirectAccess, которые применяются к любому серверу, настроенному как сервер DirectAccess в вашем развертывании. Кроме того, в них записываются правила брандмауэра Windows в режиме повышенной безопасности.

Объекты групповой политики можно создавать двумя способами:

1.  **Автоматически**. Вы можете выбрать автоматическое создание. Каждому объекту присваивается имя по умолчанию. Объекты групповой политики создаются автоматически с помощью мастера начальной настройки.

2.  **Вручную**. Вы можете использовать объекты групповой политики, предопределенные администратором Active Directory.

Учитывайте, что после настройки DirectAccess на использование определенных объектов групповой политики будет невозможно изменить выбор.

> [!IMPORTANT]
> Независимо от способа создания объектов групповой политики, если ваши клиенты используют 3G, необходимо добавить политику обнаружения медленных подключений. Путь групповая политика для **политики: настройка групповая политика медленное подключение** : **Конфигурация компьютера/политики/административные шаблоны/Система/Групповая политика**.

> [!CAUTION]
> Используйте следующую процедуру, чтобы создать резервную копию всех объектов групповая политика DirectAccess перед выполнением командлетов DirectAccess: [резервное копирование и восстановление конфигурации DirectAccess](https://go.microsoft.com/fwlink/?LinkID=257928) .

#### <a name="automatically-created-gpos"></a>Автоматически созданные объекты групповой политики
При автоматическом создании объектов групповой политики учитывайте следующее:

Автоматически созданные объекты групповой политики применяются в соответствии с их местом расположения и параметрами связи:

-   Для объектов групповой политики сервера DirectAccess место расположения и параметры связи соответствуют домену, в котором находится сервер DirectAccess.

-   При создании клиентских объектов групповой политики в качестве места расположения выбирается один целевой домен. В каждом домене происходит поиск этого объекта по имени и, если он существует, выполняется его заполнение настройками DirectAccess. GPO привязывается к корневому каталогу домена, в котором он был создан. Таким образом, объект групповой политики создается в каждом домене, в котором имеются клиентские компьютеры, и привязывается к его корневому каталогу.

Чтобы применить настройки DirectAccess при использовании автоматически созданных GPO, администратору сервера DirectAccess требуется разрешение на следующие действия:

-   Разрешение на создание GPO для каждого домена.

-   Разрешение на привязывание к корневым каталогам всех выбранных клиентских доменов.

-   Разрешение на привязывание к корневым каталогам доменов с объектами групповой политики сервера.

-   Требуются разрешения на редактирование, удаление и изменение объектов групповой политики.

-   Администратору DirectAccess рекомендуется иметь разрешение на чтение GPO для каждого необходимого домена. При создании GPO это позволяет убедиться, что не существует объектов групповой политики с одинаковыми именами.

Учитывайте, что если не существует правильных разрешений на привязывание объектов групповой политики, будет вынесено предупреждение. Работа DirectAccess продолжится, но привязывание не будет выполнено. После предупреждения будет невозможно автоматическое создание связей, даже в случае последующего добавления разрешения. Вместо этого администратору придется создавать связи вручную.

#### <a name="manually-created-gpos"></a>Объекты групповой политики, созданные вручную
При создании объектов групповой политики вручную учитывайте следующее:

-   Мастер начальной настройки удаленного доступа следует запускать, когда объекты групповой политики уже существуют.

-   При использовании объектов групповой политики, созданных вручную, для применения настроек DirectAccess администратор должен иметь все необходимые разрешения (редактирование, удаление и изменение параметров безопасности).

-   При использовании объектов групповой политики, созданных вручную, выполняется поиск связи объекта по всему домену. Если объект групповой политики не связан с доменом, он автоматически привязывается к корневому каталогу. При отсутствии разрешения на создание связей выносится предупреждение.

Учитывайте, что если не существует правильных разрешений на привязывание объектов групповой политики, будет вынесено предупреждение. Работа DirectAccess продолжится, но привязывание не будет выполнено. После предупреждения будет невозможно автоматическое создание связей, даже в случае получения разрешения в дальнейшем. Вместо этого администратору придется создавать связи вручную.

#### <a name="recovering-from-a-deleted-gpo"></a>Восстановление удаленного объекта групповой политики
Если сервер DirectAccess, клиент или объект групповой политики сервера приложений был непреднамеренно удален, и резервная копия отсутствует, необходимо удалить параметры конфигурации и выполнить настройки заново. Если имеется резервная копия, вы сможете восстановить GPO.

При **управлении DirectAccess** отобразится следующее сообщение об ошибке: **объект GPO <GPO name> не найден**. Чтобы удалить параметры конфигурации, выполните следующие действия:

1.  Запустите командлет PowerShell **Uninstall-remoteaccess**.

2.  Заново откройте консоль **Управление DirectAccess**.

3.  Отобразится сообщение об ошибке, говорящее, что GPO не найден. Щелкните **Удалить параметры конфигурации**. После этого будут восстановлены настройки сервера по умолчанию.

### <a name="next-step"></a><a name="BKMK_Links"></a>Следующий шаг

-   [Шаг 2. Планирование базового развертывания DirectAccess](da-basic-plan-s2-deployment.md)
