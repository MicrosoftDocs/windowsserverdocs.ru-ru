---
title: Планирование развертывания кластера удаленного доступа
description: Этот раздел является частью руководств по развертыванию удаленного доступа в кластере в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 88ffd598-2fde-402c-bd12-be790f84dc96
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d3765ce86bcb5552188b135c293e5eea24b0547e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963850"
---
# <a name="plan-a-remote-access-cluster-deployment"></a>Планирование развертывания кластера удаленного доступа

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

 Windows Server 2016 и Windows Server 2012 объединяют VPN-подключение DirectAccess и службы удаленного доступа (RAS) к одной роли удаленного доступа. В этом обзоре приводятся общие сведения о шагах планирования, необходимых для развертывания кластера серверов удаленного доступа Windows Server 2016 или Windows Server 2012.

-   [Спланируйте расширенное развертывание DirectAccess](../../../directaccess/single-server-advanced/Plan-an-Advanced-DirectAccess-Deployment.md). Этот шаг включает планирование инфраструктуры, необходимой для развертывания одного сервера. Он включает в себя планирование параметров сети и сервера, требования к сертификатам, параметры DNS, развертывание сервера сетевого расположения, серверы управления DirectAccess, параметры Active Directory и объекты групповая политика (GPO).

-   [Шаг 2. Планирование серверов кластера](Step-2-Plan-Cluster-Servers.md) .

-   [Шаг 3. Планирование развертывания кластера с балансировкой нагрузки](Step-3-Plan-a-Load-Balanced-Cluster-Deployment.md).

-   Шаг 4. Запишите решения по планированию для расширенного развертывания удаленного доступа. Эти данные можно использовать как задание для всех лиц, участвующих в развертывании.

После завершения этих этапов планирования см. раздел [Настройка кластера удаленного доступа](../configure/Configure-a-Remote-Access-Cluster.md).

Инструкции по настройке развертывания кластера в качестве подтверждения концепции в лабораторной среде см. в статье [Тестовая лаборатория. демонстрация DirectAccess в кластере с Windows NLB](../../../directaccess/tlg-cluster-nlb/Test-Lab-Guide-Demonstrate-DirectAccess-in-a-Cluster-with-Windows-NLB.md).



