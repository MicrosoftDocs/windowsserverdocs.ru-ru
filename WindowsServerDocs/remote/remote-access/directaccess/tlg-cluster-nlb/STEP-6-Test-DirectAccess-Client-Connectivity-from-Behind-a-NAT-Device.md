---
title: Шаг 6. Тестирование подключения клиента DirectAccess из устройства NAT
description: Узнайте, как проверить подключение к Teredo с помощью DirectAccess и подключение IP-HTTPS из устройства NAT.
manager: brianlic
ms.topic: article
ms.assetid: aded2881-99ed-4f18-868b-b765ab926597
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: f081ba36bb4bd8d13595184b058fafd1fb889778
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101834035"
---
# <a name="step-6-test-directaccess-client-connectivity-from-behind-a-nat-device"></a>Шаг 6. Тестирование подключения клиента DirectAccess из устройства NAT

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

Когда клиент DirectAccess подключается к Интернету из-за устройства NAT или сервера веб-прокси, он использует либо Teredo, либо IP-HTTPS для подключения к серверу удаленного доступа.

Если устройство NAT включает исходящий порт UDP 3544 на общедоступный IP-адрес сервера удаленного доступа, используется Teredo. Если доступ через Teredo недоступен, клиент DirectAccess возвращается к подключению IP-HTTPS через TCP-порт номер 443 исходящего трафика, который позволяет получать доступ через брандмауэр или сервер веб-прокси по традиционному SSL-порту.

Если веб-прокси требует проверки подлинности, подключение IP-HTTPS завершится сбоем. Подключение IP-HTTPS также завершится сбоем, если веб-прокси проводит проверку исходящего SSL-соединения, поскольку HTTPS-сеанс завершается на веб-прокси, а не на сервере удаленного доступа. В этом разделе будут проводиться те же тесты, которые проводятся при подключении с использованием туннеля 6to4 из предыдущего раздела.

Следующие процедуры выполняются на обоих клиентских компьютерах.

1. Проверьте подключение Teredo. Первый набор тестов выполняется, когда клиент DirectAccess настроен для использования Teredo. Это задается автоматически, если устройство NAT разрешает исходящий трафик на UDP-порт номер 3544.

2. Проверьте подключение IP-HTTPS. Второй набор тестов выполняется, когда клиент DirectAccess настроен для использования IP-HTTPS. Чтобы продемонстрировать возможность подключения IP-HTTPS, Teredo на клиентских компьютерах отключается.

> [!TIP]
> Перед выполнением этих процедур рекомендуется очистить кэш Internet Explorer, чтобы убедиться в том, что вы тестируете подключение и не получаете страницы веб-сайта из кэша.

## <a name="prerequisites"></a>Предварительные требования

Перед проведением этих тестов, отключите CLIENT1 от интернет-коммутатора и подключите его к коммутатору Homenet. Если будет задан вопрос, какой тип задать для текущей сети, выберите **Домашняя сеть**.

Запустите EDGE1 и EDGE2, если они еще не запущены.

## <a name="test-teredo-connectivity"></a>Проверка подключения Teredo

1. На компьютере КЛИЕНТ1 откройте окно Windows PowerShell с повышенными привилегиями, введите **ipconfig/all** и нажмите клавишу ВВОД.

2. Проверьте вывод команды ipconfig.

   Теперь CLIENT1 подключен к Интернету из-за устройства NAT и получил частный адрес IPv4. Когда клиент DirectAccess находится за устройством NAT и получает частный адрес IPv4, предпочитаемой технологией туннелирования для IPv6 является Teredo. Если посмотреть на вывод команды ipconfig, вы увидите раздел Туннельный адаптер Teredo Tunneling Pseudo-Interface, а также описание Туннельный адаптер Microsoft Teredo с IP-адресом, который начинается с 2001: что соответствует адресу Teredo. Если раздел Teredo отсутствует, включите Teredo следующей командой: **netsh interface Teredo set state enterpriseclient**, а затем повторно выполните команду ipconfig. Шлюза по умолчанию для туннельного адаптера Teredo не будет.

3. В окне Windows PowerShell введите **ipconfig/flushdns** и нажмите клавишу ВВОД.

   В результате будут удалены записи разрешения имен, которые могут до сих пор находиться в кэше клиента DNS со времени, когда компьютер был подключен к Интернету.

4. В окне Windows PowerShell введите **Get-днсклиентнрптполици** и нажмите клавишу ВВОД.

   В выводе появятся текущие параметры таблицы политики разрешения имен (NRPT). Эти параметры указывают, что все подключения к .corp.contoso.com должны разрешаться DNS-сервером удаленного доступа с адресом IPv6 равным 2001:db8:1::2. Кроме того, обратите внимание на запись NRPT, которая указывает на наличие исключения для имени nls.corp.contoso.com. Имена в списке исключений не получают ответа от DNS-сервера удаленного доступа. Чтобы проверить подключение к серверу удаленного доступа, можно использовать команду ping для IP-адреса DNS-сервера удаленного доступа, как ping 2001:db8:1::2 в данном примере.

5. В окне Windows PowerShell введите **ping APP1** и нажмите клавишу ВВОД. Должны появиться ответы от адреса IPv6 для APP1, 2001:db8:1::3.

6. В окне Windows PowerShell введите **ping** , а затем нажмите клавишу ВВОД. Должны появиться ответы от адреса NAT64, назначенного EDGE1 для APP2, которые в данном случае равны fdc9:9f4e:eb1b:7777::a00:4.

7. Оставьте окно Windows PowerShell открытым для следующей процедуры.

8. Откройте Internet Explorer, в адресной строке Internet Explorer введите **https://app1/** и нажмите клавишу ВВОД. Появится веб-сайт IIS на APP1 по умолчанию.

9. В адресной строке Internet Explorer введите **https://app2/** и нажмите клавишу ВВОД. Появится веб-сайт IIS на APP2 по умолчанию.

10. На **начальном** экране введите <strong> \\ \App2\Files</strong>и нажмите клавишу ВВОД. Дважды щелкните файл "Новый текстовый документ". Это показывает, что вам удалось подключиться к серверу, работающему только с адресами IPv4, с помощью SMB и получить доступ к ресурсу на узле, работающему только с адресами IPv4.

## <a name="test-ip-https-connectivity"></a>Проверка подключения IP-HTTPS

1. Откройте окно Windows PowerShell с повышенными привилегиями, введите **netsh interface Teredo Set State Disabled** и нажмите клавишу ВВОД. Это отключит Teredo на клиентском компьютере и позволит ему настроиться на использование IP-HTTPS. По завершении работы команды появится ответ **Ok**.

2. В окне Windows PowerShell введите **ipconfig/all** и нажмите клавишу ВВОД.

3. Проверьте вывод команды ipconfig. Этот компьютер теперь подключен к Интернету из-за устройства NAT и получил частный адрес IPv4. Туннелирование Teredo отключено, а клиент DirectAccess возвращается к использованию IP-HTTPS. Если посмотреть на вывод команды ipconfig, там должен быть раздел Туннельный адаптер iphttpsinterface с IP-адресом, который начинается с 2001:db8:1:100, что указывает на адрес IP-HTTPS, учитывая префикс, заданный при настройке DirectAccess. Шлюза по умолчанию для туннельного адаптера IP-HTTPS не будет.

4. В окне Windows PowerShell введите **ipconfig/flushdns** и нажмите клавишу ВВОД. В результате будут удалены записи разрешения имен, которые могут до сих пор находиться в кэше клиента DNS со времени, когда компьютер был подключен к сети предприятия.

5. В окне Windows PowerShell введите **ping APP1** и нажмите клавишу ВВОД. Должны появиться ответы от адреса IPv6 для APP1, 2001:db8:1::3.

6. В окне Windows PowerShell введите **ping** , а затем нажмите клавишу ВВОД. Должны появиться ответы от адреса NAT64, назначенного EDGE1 для APP2, которые в данном случае равны fdc9:9f4e:eb1b:7777::a00:4.

7. Откройте Internet Explorer, в адресной строке Internet Explorer введите **https://app1/** и нажмите клавишу ВВОД. Появится сайт IIS на APP1 по умолчанию.

8. В адресной строке Internet Explorer введите **https://app2/** и нажмите клавишу ВВОД. Появится веб-сайт IIS на APP2 по умолчанию.

9. На **начальном** экране введите <strong> \\ \App2\Files</strong>и нажмите клавишу ВВОД. Дважды щелкните файл "Новый текстовый документ". Это показывает, что вам удалось подключиться к серверу, работающему только с адресами IPv4, с помощью SMB и получить доступ к ресурсу на узле, работающему только с адресами IPv4.
