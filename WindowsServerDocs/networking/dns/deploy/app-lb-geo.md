---
title: Использование политики DNS для балансировки нагрузки приложений с помощью сведений о географическом расположении
description: Этот раздел является частью руководств по сценариям политики DNS для Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: b6e679c6-4398-496c-88bc-115099f3a819
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d4e005e65a3ff645ed91f488820435aff5173390
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317893"
---
# <a name="use-dns-policy-for-application-load-balancing-with-geo-location-awareness"></a>Использование политики DNS для балансировки нагрузки приложений с помощью сведений о географическом расположении

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016

С помощью этого раздела можно узнать, как настроить политику DNS для балансировки нагрузки приложения с учетом географического расположения.

В предыдущем разделе этого руководстве [используется политика DNS для балансировки нагрузки приложений](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb), используется пример вымышленной компании Contoso, которая предоставляет службы Интернет-подарков и веб-сайт с именем contosogiftservices.com. Служба "Подарочные службы Contoso" распределяет интерактивное веб-приложение между серверами в центрах обработки данных в Северной Америке, расположенных в Сиэтле, WA, Чикаго, IL и Далласе, TX.

>[!NOTE]
>Рекомендуется ознакомиться с разделом [Использование политики DNS для балансировки нагрузки приложений](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb) перед выполнением инструкций в этом сценарии.

В этом разделе используется одна и та же вымышленная компания и сетевая инфраструктура в качестве основы для нового примера развертывания, включающего сведения о географическом расположении.

В этом примере службы подарков компании Contoso успешно расширяют свое присутствие по всему миру.

Как и Северная Америка, в компании теперь есть веб-серверы, размещенные в европейских центрах обработки данных.

ИТ-администраторам Contoso необходимо настроить балансировку нагрузки приложений для европейских центров обработки данных аналогично реализации политики DNS в США, при этом трафик приложений распределяется между веб-серверами, расположенными в Дублин, Ирландия, Амстердам, Холланд и другое.

Администраторы DNS также хотят, чтобы все запросы из других расположений в мире были равномерно распределены между всеми центрами обработки данных.

В следующих разделах вы узнаете, как обеспечить выполнение аналогичных задач администраторам Contoso DNS в вашей сети.

## <a name="how-to-configure-application-load-balancing-with-geo-location-awareness"></a>Настройка балансировки нагрузки приложений с учетом географического расположения

В следующих разделах показано, как настроить политику DNS для балансировки нагрузки приложений с учетом географического расположения.

>[!IMPORTANT]
>В следующих разделах приведены примеры команд Windows PowerShell, которые содержат примеры значений для многих параметров. Перед выполнением этих команд обязательно замените примеры значений в этих командах значениями, подходящими для вашего развертывания.

### <a name="create-the-dns-client-subnets"></a><a name="bkmk_clientsubnets"></a>Создание подсетей клиента DNS

Сначала необходимо выяснить подсети или пространство IP-адресов регионов Северная Америка и Европы.

Эти сведения можно получить из карт географических IP-адресов. На основе этих дистрибутивов геоip-адресов необходимо создать подсети клиента DNS.

Подсеть клиента DNS — это логическая группа подсетей IPv4 или IPv6, из которой отправляются запросы на DNS-сервер.

Для создания подсетей клиента DNS можно использовать следующие команды Windows PowerShell. 

    
    Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet 192.0.0.0/24,182.0.0.0/24
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet 141.1.0.0/24,151.1.0.0/24
    
Дополнительные сведения см. в разделе [Add-днссерверклиентсубнет](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).

### <a name="create-the-zone-scopes"></a><a name="bkmk_zscopes2"></a>Создание областей зоны

После завершения подсетей клиента необходимо разделить зону contosogiftservices.com на разные области зоны, каждая для центра обработки данных.

Область зоны — это уникальный экземпляр зоны. Зона DNS может иметь несколько областей зоны, при этом каждая область зоны содержит собственный набор записей DNS. Одна и та же запись может присутствовать в нескольких областях с разными IP-адресами или IP-адресами.

>[!NOTE]
>По умолчанию область зоны существует в зонах DNS. Эта область зоны имеет то же имя, что и зона, а устаревшие операции DNS работают в этой области.

В предыдущем сценарии для балансировки нагрузки приложений показано, как настроить три области зоны для центров обработки данных в Северная Америка.

С помощью приведенных ниже команд можно создать две дополнительные области зоны, по одной на каждую для центров обработки данных Dublin и Амстердам. 

Вы можете добавить эти области зоны без изменений в три существующие области Северная Америка зоны в одной и той же зоне. Кроме того, после создания этих областей зоны перезагружать DNS-сервер не требуется.

Для создания областей зоны можно использовать следующие команды Windows PowerShell.

    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AmsterdamZoneScope"
    

Дополнительные сведения см. в разделе [Add-днссерверзонескопе](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps) .

### <a name="add-records-to-the-zone-scopes"></a><a name="bkmk_records2"></a>Добавление записей в области зоны

Теперь необходимо добавить записи, представляющие узел веб-сервера, в области зоны.

Записи для центров обработки данных в Америке были добавлены в предыдущем сценарии. Для добавления записей в области зоны для европейских центров обработки данных можно использовать следующие команды Windows PowerShell.
 
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "151.1.0.1" -ZoneScope "DublinZoneScope”
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "AmsterdamZoneScope"
    

Дополнительные сведения см. в разделе [Add-днссерверресаурцерекорд](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).

### <a name="create-the-dns-policies"></a><a name="bkmk_policies2"></a>Создание политик DNS

После создания разделов (областей зоны) и добавления записей необходимо создать политики DNS, которые распределяют входящие запросы между этими областями.

В этом примере распределение запросов между серверами приложений в разных центрах обработки данных соответствует следующим критериям.

1. Когда запрос DNS получен из источника в подсети клиента в Северной Америке, 50% ответов DNS указывает на центр обработки данных в Сиэтле, 25% ответов указывают на центр управления данными в Чикаго, а оставшиеся 25% ответов указывают на Datacenter в Далласе.
2. Когда запрос DNS получен из источника в Европейской подсети клиента, 50% ответов DNS указывает на центр обработки данных, а 50% ответов DNS указывает на центр обработки данных Амстердам.
3. Когда запрос поступает из любого места в мире, ответы DNS распределяются по всем пяти центрам обработки данных.

Для реализации этих политик DNS можно использовать следующие команды Windows PowerShell.

    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaLBPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1; TexasZoneScope,1" -ZoneName "contosogiftservices.com" –ProcessingOrder 1
    
    Add-DnsServerQueryResolutionPolicy -Name "EuropeLBPolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 2
    
    Add-DnsServerQueryResolutionPolicy -Name "WorldWidePolicy" -Action ALLOW -FQDN "eq,*.contoso.com" -ZoneScope "SeattleZoneScope,1;ChicagoZoneScope,1; TexasZoneScope,1;DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3
    
    

Дополнительные сведения см. в разделе [Add-днссерверкуериресолутионполици](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).

Теперь вы успешно создали политику DNS, которая обеспечивает балансировку нагрузки приложений между веб-серверами, расположенными в пяти разных центрах обработки данных на нескольких континентах.

Вы можете создавать тысячи политик DNS в соответствии с требованиями к управлению трафиком, а все новые политики применяются динамически, без перезапуска DNS-сервера во входящих запросах.
