---
title: Локальные компоненты клиента
description: Описывает локальные компоненты в развертывании служб удаленных рабочих столов.
ms.author: elizapo
ms.date: 08/01/2016
ms.topic: article
ms.assetid: b3eebb38-a835-4fa6-9e41-1966014bf2cb
author: lizap
manager: dongill
ms.openlocfilehash: e2a06368bea88a9b746242da5a0281b465804c62
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958122"
---
# <a name="tenant-on-premises-components"></a>Локальные компоненты клиента

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2019, Windows Server 2016

Следующие сведения описывают локальные компоненты, составляющие развертывание по размещению рабочих столов.

##  <a name="clients"></a>Клиенты
Чтобы получить доступ к размещенным рабочим столам и приложениям, пользователи должны использовать клиенты удаленного рабочего стола, которые поддерживают протокол удаленного рабочего стола (RDP) 7.1 или более поздней версии. В частности, клиент должен поддерживать шлюз удаленных рабочих столов и посредник подключений к удаленному рабочему столу. Для предоставления приложений на локальном рабочем столе клиент должен также поддерживать функцию RemoteApp. Чтобы добиться максимальной масштабируемости шлюза, клиент должен поддерживать чистый транспорт HTTP для подключений к шлюзу удаленных рабочих столов.

Дополнительные сведения: [Новые возможности шлюза удаленных рабочих столов в Windows Server 2012 R2](https://techcommunity.microsoft.com/t5/microsoft-security-and/what-8217-s-new-in-windows-server-2012-remote-desktop-gateway/ba-p/247611)
[Клиенты удаленного рабочего стола (Майкрософт)](./clients/remote-desktop-clients.md)
[Приложение удаленного рабочего стола для Windows в Microsoft Store](https://apps.microsoft.com/windows/app/remote-desktop/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)
[Удаленный рабочий стол — приложения для Android в Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)
[Mac App Store — удаленный рабочий стол (Майкрософт)](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417?mt=12)
[Удаленный рабочий стол (Майкрософт) в App Store](https://itunes.apple.com/app/microsoft-remote-desktop/id714464092?mt=8)

##  <a name="active-directory-domain-services"></a>Доменные службы Active Directory
Некоторые большие и более сложные клиенты могут разместить сервер доменных служб Active Directory (AD DS) в своей локальной среде. В этом случае сервер AD DS в среде клиента, как правило, будет репликой сервера AD DS, который находится в локальной среде клиента. Это поддерживается путем создания виртуальной сети в среде клиента и использования VPN-шлюза Azure для создания подключения "сеть — сеть" из локальной сети клиента к виртуальной сети клиента в центре обработки данных Azure.

Дополнительные сведения: [Обзор виртуальной сети Microsoft Azure](/azure/virtual-network/virtual-networks-overview)
[Создание виртуальной сети диспетчера ресурсов с VPN-подключением типа "сеть — сеть" с помощью портала Azure](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
