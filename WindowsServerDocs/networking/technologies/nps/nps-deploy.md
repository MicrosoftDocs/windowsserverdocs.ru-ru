---
title: Развертывание сервера политики сети
description: Этот раздел содержит ссылки на содержимое развертывания сервера политики сети для Windows Server 2016 и содержит ссылки на дополнительные рекомендации по NPS.
manager: brianlic
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 379ad808223a94abda2367a3e2184a5ff6d93f74
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97949890"
---
# <a name="deploy-network-policy-server"></a>Развертывание сервера политики сети

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Этот раздел можно использовать для получения сведений о развертывании сервера политики сети.

>[!NOTE]
>Дополнительную документацию по серверу политики сети можно получить с помощью следующих разделов библиотеки.
>- [Начало работы с сервером политики сети](nps-getstart-top.md)
>- [Планирование сервера политики сети](nps-plan-top.md)
>- [Управление сервером политики сети](nps-manage-top.md)

В сетевом каталоге Windows Server 2016 Core содержится раздел, посвященный планированию и установке сервера политики сети \( NPS \) , а технологии, представленные в этом руководства, служат предварительными требованиями для развертывания NPS в домене Active Directory. Дополнительные сведения см. в подразделе «Deploy NPS1» в [сетевом каталоге](../../core-network-guide/core-network-guide.md#BKMK_deployNPS1)Windows Server 2016 Core.

## <a name="deploy-nps-certificates-for-vpn-and-8021x-access"></a>Развертывание сертификатов NPS для доступа VPN и 802.1 X

Если требуется развернуть методы проверки подлинности, такие как \( EAP \) и Protected EAP, требующие использования сертификатов сервера в NPS, можно развернуть сертификаты NPS с помощью инструкции [Deploy Server Certificates for 802.1 x Wired and Wireless](../../core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments.md).

## <a name="deploy-nps-for-8021x-wireless-access"></a>Развертывание NPS для беспроводного доступа 802.1 X

Чтобы развернуть NPS для беспроводного доступа, воспользуйтесь руководством [deploy Password-Based 802.1 x аутентифицированный беспроводной доступ](../../core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access.md).

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Развертывание службы NPS для VPN-доступа Windows 10

NPS можно использовать для обработки запросов на подключение к Always On \( VPN-подключениям виртуальной частной сети \) для удаленных сотрудников, использующих компьютеры и устройства под управлением Windows 10.

Дополнительные сведения см. в статье [Always on удаленного доступа по развертыванию VPN для Windows Server 2016 и Windows 10](../../../remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy.md).