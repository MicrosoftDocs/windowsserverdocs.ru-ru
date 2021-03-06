---
title: Шаг 1. Настройка базовой инфраструктуры DirectAccess
description: Узнайте, как настроить инфраструктуру, необходимую для базового развертывания DirectAccess, с помощью одного сервера DirectAccess в смешанной среде IPv4 и IPv6.
manager: brianlic
ms.topic: article
ms.assetid: ba4de2a4-f237-4b14-a8a7-0b06bfcd89ad
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 0f6fc52a4b52eb513e6f7b0742ececef24fbbd3c
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101831883"
---
# <a name="step-1-configure-the-basic-directaccess-infrastructure"></a>Шаг 1. Настройка базовой инфраструктуры DirectAccess

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе описывается, как настроить инфраструктуру, необходимую для базового развертывания DirectAccess с использованием одного сервера DirectAccess в смешанной среде с поддержкой IPv4 и IPv6. Прежде чем приступить к развертыванию, убедитесь, что выполнены действия по планированию, описанные в разделе [планирование базового развертывания DirectAccess](../../../remote-access/directaccess/single-server-wizard/Plan-a-Basic-DirectAccess-Deployment.md).

|Задача|Описание|
|----|--------|
|Настройка сетевых параметров сервера|Настройте сетевые параметры на сервере DirectAccess.|
|Настройте маршрутизацию в корпоративной сети|Для правильного направления трафика следует настроить маршрутизацию в корпоративной сети.|
|Настройка брандмауэров|При необходимости настройте дополнительные брандмауэры.|
|Настройка DNS-сервера|Настройте параметры DNS для сервера DirectAccess.|
|Настройка Active Directory|Присоедините клиентские компьютеры и сервер DirectAccess к домену Active Directory.|
|Настройка объектов групповой политики|Если необходимо, настройте объекты групповой политики для развертывания.|
|Настройка групп безопасности|Настройте группы безопасности, включающие компьютеры клиентов DirectAccess, а также любые другие группы безопасности, необходимые для развертывания.|

> [!NOTE]
> В этом разделе приводятся примеры командлетов Windows PowerShell, которые можно использовать для автоматизации некоторых описанных процедур. Дополнительные сведения см. в разделе [Использование командлетов](https://go.microsoft.com/fwlink/p/?linkid=230693).

## <a name="configure-server-network-settings"></a><a name="ConfigNetworkSettings"></a>Настройка сетевых параметров сервера
Для развертывания одиночного сервера в среде, работающей на основе IPv4 и IPv6, необходимо выполнить следующие настройки сетевого интерфейса: Для настройки всех IP-адресов используется пункт **Изменение параметров адаптера** в разделе **Центр управления сетями и общим доступом Windows**.

-   Пограничная топология

    -   Один общедоступный статический IPv4- или IPv6-адрес для Интернета.

        > [!NOTE]
        > Для Teredo необходимы два последовательных общедоступных IPv4-адреса. Если вы не используете Teredo, вы можете настроить один общедоступный статичный IPv4-адрес.

    -   Один внутренний статический IPv4- или IPv6-адрес.

-   За устройством NAT (два сетевых адаптера)

    -   Один внутренний IPv4- или IPv6-адрес, направленный в Интернет.

    -   Один статический IPv4- или IPv6-адрес для сети периметра.

-   За устройством NAT (один сетевой адаптер)

    -   Один статический IPv4- или IPv6-адрес.

> [!NOTE]
> Если сервер DirectAccess оснащен двумя или более сетевыми адаптерами (один указан в доменном профиле, а другой — в публичном или частном), но планируется использование топологии с одной сетевой картой, следует выполнить следующие действия.
>
> 1.  Убедитесь, что второй сетевой адаптер и все дополнительные адаптеры определены в профиле домена.
> 2.  Если второй сетевой адаптер по какой-либо причине не может быть настроен для доменного профиля, следует вручную установить область действия политик IPsec DirectAccess для всех профилей с помощью следующих команд Windows PowerShell.
>
>     ```
>     $gposession = Open-NetGPO -PolicyStore <Name of the server GPO>
>     Set-NetIPsecRule -DisplayName <Name of the IPsec policy> -GPOSession $gposession -Profile Any
>     Save-NetGPO -GPOSession $gposession
>     ```
>
>     Политики IPsec — DirectAccess-DaServerToInfra и DirectAccess-DaServerToCorp.

## <a name="configure-routing-in-the-corporate-network"></a><a name="ConfigRouting"></a>Настройте маршрутизацию в корпоративной сети
Настройте маршрутизацию в корпоративной сети следующим образом.

-   Если в организации развернута собственная инфраструктура на основе IPv6, следует добавить маршрут, позволяющий маршрутизаторам, расположенным во внутренней сети, возвращать трафик IPv6 через сервер удаленного доступа.

-   Вручную настройте маршруты IPv4 и IPv6 на серверах удаленного доступа. Добавьте опубликованный маршрут, чтобы весь трафик с префиксом IPv6 организации (/48) пересылался во внутреннюю сеть Кроме того, следует добавить подробные маршруты для направления IPv4-трафика во внутреннюю сеть.

## <a name="configure-firewalls"></a><a name="ConfigFirewalls"></a>Настройка брандмауэров
Если вы используете при развертывании дополнительные брандмауэры, примените следующие исключения для трафика удаленного доступа при выходе в Интернет, когда сервер удаленного доступа находится в сети IPv4:

-   трафик 6to4 — IP-протокол 41, входящий и исходящий.

-   Протокол IP-HTTPS — порт назначения TCP 443 и порт источника TCP 443 исходящие. Когда сервер удаленного доступа имеет один сетевой адаптер, а сервер сетевых расположений находится на сервере удаленного доступа, тогда также требуется TCP-порт 62000.

    > [!NOTE]
    > Это исключение должно быть настроено на сервере удаленного доступа. Все остальные исключения должны быть настроены на пограничном брандмауэре.

> [!NOTE]
> В отношении трафика Teredo и 6to4 эти исключения должны применяться для обоих последовательных общедоступных IPv4-адресов для выхода в Интернет на сервере удаленного доступа. Для IP-HTTPS исключения необходимо применять к тому адресу, которому соответствует внешнее имя сервера.

Если вы используете дополнительные брандмауэры, примените следующие исключения брандмауэра для трафика удаленного доступа при выходе в Интернет, когда сервер удаленного доступа находится в сети IPv6:

-   Протокол IP 50

-   UDP-порт назначения 500 для входящих подключений и UDP-порт источника 500 для исходящих подключений.

При использовании дополнительных брандмауэров применяйте следующие исключения внутреннего сетевого брандмауэра для трафика удаленного доступа:

-   ISATAP — протокол 41, входящий и исходящий

-   Протоколы TCP/UDP для всех типов трафика IPv4/IPv6

## <a name="configure-the-dns-server"></a><a name="ConfigDNS"></a>Настройка DNS-сервера
Необходимо вручную настроить запись DNS для веб-сайта сервера сетевых расположений внутренней сети в вашем развертывании.

### <a name="to-create-the-network-location-server-and-ncsi-probe-dns-records"></a><a name="NLS_DNS"></a>Создание сервера сетевых расположений DNS-записей NCSI-пробы

1.  На DNS-сервере внутренней сети запустите **днсмгмт. msc** и нажмите клавишу ВВОД.

2.  В левой области консоли **Диспетчер DNS** разверните зону прямого просмотра для вашего домена. Щелкните правой кнопкой мыши по домену и выберите **Новый узел (A или AAAA)**.

3.  В диалоговом окне **Новый узел** в поле **Имя (если не указано, используется родительский домен)** укажите имя DNS для веб-сайта сервера сетевых расположений (это имя используется клиентами DirectAccess для подключения к серверу сетевых расположений). В поле **IP-адрес** укажите IPv4-адрес сервера сетевых расположений и нажмите **Добавить узел**. В диалоговом окне **DNS** щелкните **OK**.

4.  В диалоговом окне **Новый узел** в поле **Имя (если не указано, используется родительский домен)** укажите имя DNS для веб-пробы (имя веб-пробы по умолчанию: directaccess-webprobehost). В поле **IP-адрес** укажите IPv4-адрес веб-пробы и щелкните **Добавить узел**. Повторите этот процесс для имени directaccess-corpconnectivityhost и любых средств проверки подключения, созданных вручную. В диалоговом окне **DNS** щелкните **OK**.

5.  Нажмите кнопку **Done**(Готово).

![](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)***<em>Эквивалентные команды</em> в Windows PowerShell Windows PowerShell***

Следующие командлеты Windows PowerShell выполняют ту же функцию, что и предыдущая процедура. Вводите каждый командлет в одной строке, несмотря на то, что здесь они могут отображаться разбитыми на несколько строк из-за ограничений форматирования.

```
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>
```

Также следует настроить записи DNS для следующих компонентов:

-   **Сервер IP-HTTPS** — клиенты DirectAccess должны иметь возможность разрешить DNS-имя сервера удаленного доступа из Интернета.

-   **Проверка отзыва списка отзыва сертификатов** . DirectAccess использует проверку отзыва сертификатов для подключения IP-HTTPS между клиентами DirectAccess и сервером удаленного доступа, а также для подключения на основе протокола HTTPS между клиентом DirectAccess и сервером сетевого расположения. В обоих случаях у клиентов DirectAccess должна быть возможность разрешения расположения точки распространения CRL и доступа к ней.

## <a name="configure-active-directory"></a><a name="ConfigAD"></a>Настройка Active Directory
Сервер удаленного доступа и клиентские компьютеры DirectAccess должны принадлежать домену Active Directory. Клиентские компьютеры DirectAccess должны быть членом домена одного из следующих типов:

-   Домены, принадлежащие к тому же лесу, что и сервер удаленного доступа.

-   Домены, принадлежащие к лесам, имеющим двустороннее доверие с лесом сервера удаленного доступа.

-   Домены, имеющие двустороннее доверие с доменом сервера удаленного доступа.

#### <a name="to-join-the-remote-access-server-to-a-domain"></a>Присоединение сервера удаленного доступа к домену

1.  В диспетчере серверов щелкните **Локальный сервер**. В области сведений перейдите по ссылке **Имя компьютера**.

2.  В диалоговом окне **Свойства системы** перейдите на вкладку **имя компьютера** . На вкладке **имя компьютера** нажмите кнопку **изменить**.

3.  В поле **Имя компьютера** введите имя компьютера, если вы меняете имя компьютера при присоединении сервера к домену. В разделе **Член групп** выберите **Домен** и введите имя домена, к которому нужно присоединить сервер, например corp.contoso.com, а затем нажмите **ОК**.

4.  При появлении предложения ввести имя пользователя и пароль введите имя и пароль пользователя с правами присоединения компьютеров к домену, а затем нажмите **ОК**.

5.  При появлении диалогового окна с приветствием домена нажмите кнопку **"OK"**.

6.  При появлении запроса на перезагрузку компьютера нажмите кнопку **ОК**.

7.  В диалоговом окне **Свойства системы** нажмите **Закрыть**.

8.  При появлении запроса на перезагрузку компьютера нажмите кнопку **Перезагрузить сейчас**.

#### <a name="to-join-client-computers-to-the-domain"></a>Присоединение клиентских компьютеров к домену

1.  Запустите **explorer.exe**.

2.  Щелкните правой кнопкой значок компьютера и выберите **Свойства**.

3.  На странице **Система** щелкните **Дополнительные параметры системы**.

4.  В диалоговом окне **Свойства системы** на вкладке **Имя компьютера** щелкните **Изменить**.

5.  В поле **Имя компьютера** введите имя компьютера, если вы меняете имя компьютера при присоединении сервера к домену. В разделе **Член групп** выберите **Домен** и введите имя домена, к которому нужно присоединить сервер, например corp.contoso.com, а затем нажмите **ОК**.

6.  При появлении предложения ввести имя пользователя и пароль введите имя и пароль пользователя с правами присоединения компьютеров к домену, а затем нажмите **ОК**.

7.  При появлении диалогового окна с приветствием домена нажмите кнопку **"OK"**.

8.  При появлении запроса на перезагрузку компьютера нажмите кнопку **ОК**.

9. В диалоговом окне **Свойства системы** нажмите кнопку "Закрыть". Щелкните **Перезагрузить сейчас**, когда появится сообщение о необходимости перезагрузки.

![](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)***<em>Эквивалентные команды</em> в Windows PowerShell Windows PowerShell***

Следующие командлеты Windows PowerShell выполняют ту же функцию, что и предыдущая процедура. Вводите каждый командлет в одной строке, несмотря на то, что здесь они могут отображаться разбитыми на несколько строк из-за ограничений форматирования.

Обратите внимание, что после введения команды "Добавить компьютер" необходимо ввести учетные данные домена.

```
Add-Computer -DomainName <domain_name>
Restart-Computer
```

## <a name="configure-gpos"></a><a name="ConfigGPOs"></a>Настройка объектов групповой политики
Для развертывания удаленного доступа требуется как минимум два объекта групповой политики: один объект групповой политики содержит параметры для сервера удаленного доступа, а один — параметры для клиентских компьютеров DirectAccess. При настройке удаленного доступа мастер автоматически создает требуемый объект групповой политики. Однако если ваша организация применяет Соглашение об именовании или у вас нет необходимых разрешений для создания или изменения объектов групповой политики, они должны быть созданы перед настройкой удаленного доступа.

Сведения о создании объекта групповой политики см. в разделе [Создание и изменение объекта Групповая политика](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754740(v=ws.11)).

> [!IMPORTANT]
> Администратор может вручную связать объект групповой политики DirectAccess с подразделением, выполнив следующие действия:
>
> 1.  Перед настройкой DirectAccess свяжите созданные объекты групповой политики с соответствующими подразделениями.
> 2.  Настройте DirectAccess, укажите группу безопасности для клиентских компьютеров.
> 3.  У администратора могут как иметься, так и отсутствовать разрешения связывать объекты групповой политики с доменом. В любом из этих случаев объекты групповой политики будут настроены автоматически. Если объекты групповой политики уже привязаны к подразделению, связи не будут удалены, а объекты групповой политики не будут связаны с доменом. Для объекта групповой политики сервера подразделение должно содержать объект-компьютер сервера. В противном случае объект групповой политики будет связан с корневым каналом домена.
> 4.  После завершения настройки администратор домена также может связать объекты групповой политики DirectAccess с необходимыми подразделениями, если это не было сделано до запуска мастера DirectAccess. Связь с доменом можно удалить. Действия по связыванию объекта групповой политики с подразделением можно найти [здесь](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732979(v=ws.11)) .

> [!NOTE]
> Если объект групповой политики был создан вручную, то во время настройки DirectAccess возможно, что объект групповой политики будет недоступен. Возможно, объект групповой политики не был реплицирован на ближайший контроллер домена на компьютер управления. В этом случае администратор может дождаться завершения репликации или выполнить принудительную репликацию.

> [!Warning]
> Использование любых средств, кроме мастера установки DirectAccess, для настройки DirectAccess, таких как изменение объектов DirectAccess групповая политика напрямую или изменение параметров политики по умолчанию на сервере или клиенте вручную, не поддерживается.

## <a name="configure-security-groups"></a><a name="ConfigSGs"></a>Настройка групп безопасности
Параметры DirectAccess, содержащиеся в объектах групповой политики клиентского компьютера, применяются только к компьютерам, входящим в группы безопасности, указанные при настройке удаленного доступа.

### <a name="to-create-a-security-group-for-directaccess-clients"></a><a name="Sec_Group"></a>Создание группы безопасности для клиентов DirectAccess

1.  Запустите **DSA. msc**. В консоли **Active Directory — пользователи и компьютеры** разверните в левой области домен, к которому будет принадлежать группа безопасности, щелкните правой кнопкой мыши **Пользователи**, выберите **Новые**, после чего щелкните **Группа**.

2.  В диалоговом окне **Создать объект — Группа** в поле **Имя группы** укажите имя группы безопасности.

3.  Параметру **Область действия группы** присвойте значение **Глобальная**, параметру **Тип группы** — значение **Безопасность**, после чего нажмите **OK**.

4.  Дважды щелкните по группе безопасности, в которую входят компьютеры клиентов DirectAccess, и в диалоговом окне со свойствами откройте вкладку **Члены**.

5.  На вкладке **Члены группы** щелкните **Добавить**.

6.  В диалоговом окне **Выбор пользователей, контактов, компьютеров, учетных записей служб или групп** выберите клиентские компьютеры, для которых хотите установить DirectAccess, после чего щелкните **OK**.

![](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)**Эквивалентные команды** в Windows PowerShell Windows PowerShell

Следующие командлеты Windows PowerShell выполняют ту же функцию, что и предыдущая процедура. Вводите каждый командлет в одной строке, несмотря на то, что здесь они могут отображаться разбитыми на несколько строк из-за ограничений форматирования.

```
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>
```

## <a name="next-step"></a><a name="BKMK_Links"></a>Следующий шаг

-   [Шаг 2. Настройка базового сервера DirectAccess](da-basic-configure-s2-server.md)

