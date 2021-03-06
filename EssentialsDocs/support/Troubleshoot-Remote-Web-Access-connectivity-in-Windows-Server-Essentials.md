---
title: Устранение неполадок подключения к системе удаленного веб-доступа в Windows Server Essentials
description: Узнайте, как устранять неполадки подключения удаленного Веб-доступ в Windows Server Essentials.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: d3642575-b3ee-4488-b654-5bf9d3b8c935
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: c73283d60d2286ef9e04b4ad2d1bd747cc2d6e98
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810241"
---
# <a name="troubleshoot-remote-web-access-connectivity-in-windows-server-essentials"></a>Устранение неполадок подключения к системе удаленного веб-доступа в Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Как правило, Windows Server Essentials может автоматически настроить маршрутизатор широкополосной связи, если этот маршрутизатор является сертифицированным устройством UPnP и на нем включен параметр UPnP.

## <a name="possible-issues"></a>Возможные проблемы
 Возможны следующие проблемы с подключением удаленного веб-доступа.

-   Маршрутизатор не включен или не подключен к корпоративной сети.

-   На маршрутизаторе выключен параметр UPnP.

-   Возможно, маршрутизатор не полностью поддерживает стандарт UPnP. В корпорации Майкрософт существует список маршрутизаторов, работающих с операционными системами Windows. Чтобы просмотреть список маршрутизаторов (включая беспроводные маршрутизаторы), совместимых с Windows Server Essentials, посетите [Центр совместимости Windows](https://www.microsoft.com/windows/compatibility/CompatCenter/Home).

## <a name="possible-fixes"></a>Возможные исправления
 Эти проблемы можно устранить с помощью следующих действий.

- Убедитесь, что маршрутизатор включен и работает надлежащим образом.

- Убедитесь, что сервер подключен непосредственно к маршрутизатору либо к коммутатору, который, в свою очередь, подключен к маршрутизатору.

- Убедитесь, что устройство широкополосной связи, которое подключается к поставщику услуг Интернета, включено и работает, а маршрутизатор подключен к этому устройству.

- Включите параметр UPnP на маршрутизаторе Чтобы включить параметр UPnP, подключитесь к веб-странице конфигурации маршрутизатора. Сведения о входе на маршрутизатор и включении параметра UPnP см. в документации по маршрутизатору. После включения параметра UPnP снова запустите мастер включения удаленного Веб-доступ, чтобы настроить маршрутизатор.

- Если маршрутизатор не полностью поддерживает стандарт UPnP, его нельзя настроить автоматически. Необходимо вручную настроить маршрутизатор или приобрести маршрутизатор, который поддерживает стандарт UPnP.

   Чтобы настроить маршрутизатор вручную, необходимо выполнить следующие задачи.

  - Создайте резервирование IP-адреса для сервера Windows Server Essentials.

     Прежде чем вручную настроить маршрутизатор для пересылки необходимых портов в Windows Server Essentials, на маршрутизаторе необходимо задать резервирование DHCP-протокола для сервера, на котором работает Windows Server Essentials. Это гарантирует, что IP-адрес, на который будут пересылаться порты, не изменится.

     Сведения о том, как вручную настроить резервирование DHCP для сервера на маршрутизаторе, см. в документации изготовителя для своего маршрутизатора.

  - Настройте перенаправление портов на маршрутизаторе для следующих портов.

    |Служба или протокол|Порт|
    |-------------------------|----------|
    |HTTP|TCP 80|
    |HTTPS|TCP 443|

    Сведения о настройке перенаправления портов на маршрутизаторе вручную см. в документации производителя.

    На странице конфигурирования маршрутизатора обычно находится таблица, которая содержит следующие данные.

  > [!NOTE]
  >  В этой таблице IP-адрес компьютера с Windows Server Essentials — 192.168.0.100. Необходимо определить IP-адрес вашего компьютера и заменить его на IP-адреса, указанный в таблице.

  |IP-адрес|Протокол (TCP/UDP)|Расписание|Входящий фильтр|
  |----------------|---------------------------|--------------|--------------------|
  |192.168.0.100|TCP 80|Всегда|Разрешить все|
  |192.168.0.100|TCP 443|Всегда|Разрешить все|

   После ручной настройки маршрутизатора запустите мастер включения удаленного Веб-доступ, убедившись, что на странице **Приступая к работе** установлен флажок **пропустить установку маршрутизатора** .

- Приобретите новый маршрутизатор, если существующее устройство не полностью поддерживает стандарт UPnP.

> [!TIP]
>  Убедитесь, что на маршрутизаторе установлена последняя версия встроенного ПО BIOS. Обновить встроенное ПО BIOS для маршрутизатора можно с веб-страницы настройки маршрутизатора. Дополнительные сведения см. в документации к маршрутизатору. После обновления маршрутизатора запустите мастер настройки повсеместного доступа.

## <a name="see-also"></a>См. также раздел

-   [Раздел об использовании удаленного веб-доступа](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [Управление удаленным веб-доступом](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [Управление повсеместным доступом](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Управление Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)

-   [Поддержка Windows Server Essentials](../support/Support-Windows-Server-Essentials.md)

