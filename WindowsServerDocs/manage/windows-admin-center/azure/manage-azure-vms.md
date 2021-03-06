---
title: Управление виртуальными машинами Azure IaaS
description: Управление виртуальными машинами Azure IaaS с помощью центра администрирования Windows
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 02/18/2021
ms.localizationpriority: medium
ms.openlocfilehash: 93fdfdf4b5f90112b609c6f2a4d7cf58f72a9455
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101830755"
---
# <a name="manage-azure-virtual-machines-with-windows-admin-center"></a>Управление виртуальными машинами Azure с помощью центра администрирования Windows

В этой статье описывается, как использовать центр администрирования Windows, работающий на локальном компьютере или сервере, для управления операционной системой на одной или нескольких виртуальных машинах Azure (в дополнение к локальным серверам, компьютерам и виртуальным машинам).

Чтобы вместо этого использовать центр администрирования Windows непосредственно в портал Azure для управления операционной системой на отдельной виртуальной машине Azure, см. статью [Использование центра администрирования Windows в Azure](manage-vm.md). Вы также можете использовать сценарии для [настройки сервера центра администрирования Windows на виртуальной машине Azure](deploy-wac-in-azure.md).

## <a name="connecting-to-vms-with-a-public-ip"></a>Подключение к виртуальным машинам с общедоступным IP-адресом

Если ваши целевые виртуальные машины (виртуальные машины, которыми вы хотите управлять с помощью центра администрирования Windows) имеют общедоступные IP-адреса, добавьте их в шлюз центра администрирования Windows, используя IP или полное доменное имя (FQDN). Необходимо учитывать несколько моментов.

- Необходимо включить доступ WinRM к целевой виртуальной машине, выполнив следующую команду в PowerShell или в командной строке на целевой виртуальной машине: `winrm quickconfig`
- Если вы еще не присоединились к доменной виртуальной машине Azure, виртуальная машина ведет себя как сервер в Рабочей группе, поэтому необходимо убедиться, что учетная запись [используется в качестве центра администрирования Windows в Рабочей группе](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup).
- Необходимо также включить входящие подключения к порту 5985 для WinRM по протоколу HTTP, чтобы центр администрирования Windows мог управлять целевой виртуальной машиной.
  1. Выполните следующий сценарий PowerShell на целевой виртуальной машине, чтобы включить входящие подключения к порту 5985 в гостевой ОС: `Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any`

  2. Также необходимо открыть порт в сети Azure:

     - Выберите виртуальную машину Azure, выберите **сети**, а затем **Добавьте правило для входящего порта**.
     - Убедитесь, что в верхней части панели **Добавить правило безопасности для входящего трафика** выбран **базовый** .
     - В поле **диапазоны портов** введите **5985**.

     Если у шлюза центра администрирования Windows есть статический IP-адрес, можно разрешить только входящий доступ к WinRM из шлюза центра администрирования Windows для повышения безопасности.
     Для этого в верхней части панели **Добавление правила безопасности для входящего трафика** выберите **Дополнительно** .

     В поле **источник** выберите **IP-адреса**, а затем введите исходный IP-адрес, соответствующий вашему шлюзу центра администрирования Windows.

     - В качестве **протокола** выберите **TCP**.
     - Остальные можно оставить по умолчанию.

> [!NOTE]
> Необходимо создать настраиваемое правило порта. Правило порта WinRM, предоставляемое сетью Azure, использует порт 5986 (по протоколу HTTPS) вместо 5985 (по протоколу HTTP).

## <a name="connecting-to-vms-without-a-public-ip"></a>Подключение к виртуальным машинам без общедоступного IP-адреса

Если целевые виртуальные машины Azure не имеют общедоступных IP-адресов и вы хотите управлять этими виртуальными машинами из шлюза центра администрирования Windows, развернутого в локальной сети, необходимо настроить локальную сеть для подключения к виртуальной сети, в которой подключены целевые виртуальные машины. Это можно сделать тремя способами: ExpressRoute, VPN типа "сеть — сеть" или VPN-подключение типа "точка — сеть". [Узнайте, какой вариант подключения имеет смысл в вашей среде.](/azure/vpn-gateway/vpn-gateway-plan-design)

>[!TIP]
>Если вы хотите использовать VPN-подключение типа "точка — сеть" для подключения шлюза центра администрирования Windows к виртуальной сети Azure для управления виртуальными машинами Azure в этой виртуальной сети, можно использовать функцию [сетевого адаптера Azure](https://aka.ms/WACNetworkAdapter) в центре администрирования Windows. Для этого подключитесь к серверу, на котором установлен центр администрирования Windows, перейдите к средству "сеть" и выберите "добавить сетевой адаптер Azure". Когда вы укажете необходимые сведения и наберете "настроить", центр администрирования Windows настроит VPN-подключение типа "точка — сеть" с указанной виртуальной сетью Azure, после чего вы сможете подключиться к виртуальным машинам Azure и управлять ими из локального шлюза центра администрирования Windows.

Убедитесь, что служба WinRM выполняется на целевых виртуальных машинах, выполнив следующую команду в PowerShell или в командной строке на целевой виртуальной машине: `winrm quickconfig`

Если вы еще не присоединились к доменной виртуальной машине Azure, виртуальная машина ведет себя как сервер в Рабочей группе, поэтому необходимо убедиться, что учетная запись [используется в качестве центра администрирования Windows в Рабочей группе](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup).

При возникновении проблем обратитесь к разделу [Устранение неполадок в центре администрирования Windows](../support/troubleshooting.md) , чтобы узнать, требуются ли дополнительные действия для настройки (например, если вы подключаетесь с помощью учетной записи локального администратора или не присоединены к домену).
