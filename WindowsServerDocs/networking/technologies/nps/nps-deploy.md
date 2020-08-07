---
title: Развертывание сервера политики сети
description: Этот раздел содержит ссылки на содержимое развертывания сервера политики сети для Windows Server 2016 и содержит ссылки на дополнительные рекомендации по NPS.
manager: brianlic
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: lizross
author: eross-msft
ms.openlocfilehash: b4f80d18b2facba7bb706bb566aed698c2a85c8d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937415"
---
# <a name="deploy-network-policy-server"></a>Развертывание сервера политики сети

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Этот раздел можно использовать для получения сведений о развертывании сервера политики сети.

>[!NOTE]
>Дополнительную документацию по серверу политики сети можно получить с помощью следующих разделов библиотеки.
>- [Начало работы с сервером политики сети](nps-getstart-top.md)
>- [Планирование сервера политики сети](nps-plan-top.md)
>- [Управление сервером политики сети](nps-manage-top.md)

В сетевом каталоге Windows Server 2016 Core содержится раздел, посвященный планированию и установке сервера политики сети \( NPS \) , а технологии, представленные в этом руководства, служат предварительными требованиями для развертывания NPS в домене Active Directory. Дополнительные сведения см. в подразделе «Deploy NPS1» в [сетевом каталоге](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployNPS1)Windows Server 2016 Core.

## <a name="deploy-nps-certificates-for-vpn-and-8021x-access"></a>Развертывание сертификатов NPS для доступа VPN и 802.1 X

Если требуется развернуть методы проверки подлинности, такие как \( EAP \) и Protected EAP, требующие использования сертификатов сервера в NPS, можно развернуть сертификаты NPS с помощью инструкции [Deploy Server Certificates for 802.1 x Wired and Wireless](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments).

## <a name="deploy-nps-for-8021x-wireless-access"></a>Развертывание NPS для беспроводного доступа 802.1 X

Чтобы развернуть NPS для беспроводного доступа, можно воспользоваться руководством [развертывание беспроводного доступа 802.1 x с проверкой подлинности на основе пароля](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access).

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Развертывание службы NPS для VPN-доступа Windows 10

NPS можно использовать для обработки запросов на подключение к Always On \( VPN-подключениям виртуальной частной сети \) для удаленных сотрудников, использующих компьютеры и устройства под управлением Windows 10.

Дополнительные сведения см. в статье [Always on удаленного доступа по развертыванию VPN для Windows Server 2016 и Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy).

