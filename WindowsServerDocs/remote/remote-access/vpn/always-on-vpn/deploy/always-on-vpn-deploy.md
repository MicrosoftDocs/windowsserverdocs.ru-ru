---
title: Развертывание постоянно подключенного VPN-профиля для Windows Server и Windows 10
description: Это развертывание можно использовать для развертывания Always On VPN-подключений для удаленных сотрудников с помощью удаленного доступа в Windows Server 2016 или более поздней версии и Always On профилей VPN для клиентских компьютеров Windows 10.
ms.topic: article
ms.assetid: 5ae1a40b-4f10-4ace-8aaf-13f7ab581f4f
ms.localizationpriority: medium
ms.date: 12/20/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.openlocfilehash: bc7608d71dcb2bce19138fea18d6de23cda97d35
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963790"
---
# <a name="always-on-vpn-deployment-for-windows-server-and-windows-10"></a>Развертывание Always On VPN для Windows Server и Windows 10

>Область применения: Windows Server (половина ежегодного канала), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Назад:** Удаленный доступ](../../../Remote-Access.md)<br>
- [**Далее:** Дополнительные сведения о функциях и функциях VPN Always On](../../vpn-map-da.md)

Always On VPN предоставляет единое, единое решение для удаленного доступа и поддерживает присоединенные к домену, не присоединенные к домену (workgroup) или присоединенные к Azure AD устройства, даже персональные устройства. Благодаря Always On VPN соединение может предназначаться не только для пользователя или устройства, но и для них обоих. Например, можно включить аутентификацию устройств для управления удаленными устройствами, а затем включить аутентификацию пользователей для подключений к внутренним сайтам и службам компании.

## <a name="prerequisites"></a>Предварительные требования

Скорее всего, развернуты технологии, которые можно использовать для развертывания Always On VPN. Кроме серверов DC/DNS, для развертывания Always On VPN требуется сервер NPS (RADIUS), сервер центра сертификации (ЦС) и сервер удаленного доступа (маршрутизация/VPN). После настройки инфраструктуры необходимо зарегистрировать клиенты, а затем безопасно подключить клиенты к локальной сети с помощью нескольких сетевых изменений.

- Active Directory доменной инфраструктуре, включая один или несколько DNS-серверов. Требуются как внутренние, так и внешние зоны службы доменных имен (DNS), что предполагает, что внутренняя зона является делегированным поддоменом внешней зоны (например, corp.contoso.com и contoso.com).
- Инфраструктура открытых ключей (PKI) на основе Active Directory и Active Directory служб сертификации (AD CS).
- Для установки сервера политики сети (NPS): виртуальный или физический, существующий или новый. Если у вас уже есть серверы NPS в сети, можно изменить существующую конфигурацию сервера NPS, а не добавить новый сервер.
- Удаленный доступ в качестве VPN-сервера шлюза RAS с небольшим набором функций, поддерживающих VPN-подключения по протоколу IKEv2 и маршрутизацию локальной сети.
- Сеть периметра, которая включает два брандмауэра.  Убедитесь, что брандмауэры разрешают правильную работу трафика, необходимого для подключения VPN и RADIUS. Дополнительные сведения см. в статье [Always on общие сведения о технологии VPN](../always-on-vpn-technology-overview.md).
- Физический сервер или виртуальная машина в сети периметра с двумя физическими сетевыми адаптерами Ethernet для установки удаленного доступа в качестве VPN-сервера шлюза RAS. Для виртуальных машин требуется виртуальная локальная сеть (VLAN) для узла.
- Членство в группах «Администраторы» или «эквивалентное» является минимальным необходимым.
- Ознакомьтесь с разделом Планирование этого руководством, чтобы убедиться, что вы готовы к развертыванию, прежде чем выполнять развертывание.
- Ознакомьтесь с руководством по проектированию и развертыванию для каждой из используемых технологий. Эти руководства помогут определить, предоставляют ли сценарии развертывания службы и конфигурацию, необходимые для сети Организации. Дополнительные сведения см. в статье [Always on общие сведения о технологии VPN](../always-on-vpn-technology-overview.md).
- Выбранная платформа управления для развертывания конфигурации Always On VPN, так как CSP не зависит от поставщика.

>[!IMPORTANT]
>Для этого развертывания не требуется, чтобы серверы инфраструктуры, например компьютеры под управлением домен Active Directory Services, Active Directory службы сертификатов и сервер политики сети, выполнялись под управлением Windows Server 2016. Можно использовать более ранние версии Windows Server, такие как Windows Server 2012 R2, для серверов инфраструктуры и для сервера, на котором выполняется удаленный доступ.
>
>Не пытайтесь развернуть удаленный доступ на виртуальной машине (ВМ) в Microsoft Azure. Использование удаленного доступа в Microsoft Azure не поддерживается, включая VPN удаленного доступа и DirectAccess. Дополнительные сведения см. в [статье поддержка серверного программного обеспечения Майкрософт для Microsoft Azure виртуальных машин](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

## <a name="about-this-deployment"></a>Об этом развертывании

Приведенные инструкции описывают развертывание удаленного доступа в качестве VPN-шлюза для подключения типа "точка — сеть" с помощью любого из сценариев, упомянутых ниже, для удаленных клиентских компьютеров под управлением Windows 10. Кроме того, вы найдете инструкции по изменению некоторых существующих инфраструктур для развертывания. Кроме того, в рамках этого развертывания вы найдете ссылки на дополнительные сведения о процессе VPN-подключения, серверах для настройки, Профилексмл поддержка vpnv2 node и других технологиях развертывания Always On VPN.

**Always On сценарии развертывания VPN:**

1. Развертывание только Always On VPN.
2. Развертывание Always On VPN с условным доступом для VPN-подключения с помощью Azure AD.

Дополнительные сведения и рабочий процесс приведенных сценариев см. в разделе [Deploy Always on VPN](always-on-vpn-deploy-deployment.md).

## <a name="what-isnt-provided-in-this-deployment"></a>Что не предусмотрено в этом развертывании

Это развертывание не предоставляет инструкции для:

- Службы домен Active Directory (AD DS).
- Службы сертификатов Active Directory (AD CS) и инфраструктура открытых ключей (PKI).
- Протокол DHCP.
- Сетевое оборудование, например кабель Ethernet, брандмауэры, коммутаторы и концентраторы.
- Дополнительные сетевые ресурсы, например приложения и файловые серверы, к которым удаленные пользователи могут получить доступ через Always On VPN-подключение.
- Подключение к Интернету или условный доступ для подключения к Интернету с помощью Azure AD. Дополнительные сведения см. [в разделе условный доступ в Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal).

## <a name="next-steps"></a>Дальнейшие действия

- [Дополнительные сведения о функциях и функциях VPN Always On](../../vpn-map-da.md)

- [Дополнительные сведения об улучшениях Always On VPN](../always-on-vpn-enhancements.md)

- [Сведения о некоторых дополнительных функциях VPN Always On](always-on-vpn-adv-options.md)

- [Дополнительные сведения о технологии VPN Always On](../always-on-vpn-technology-overview.md)

- [Начало планирования развертывания Always On VPN](always-on-vpn-deploy-deployment.md)
