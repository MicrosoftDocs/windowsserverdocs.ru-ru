---
title: Планирование развертывания кластера удаленного доступа
description: Узнайте о шагах планирования, необходимых для развертывания кластера серверов удаленного доступа Windows Server 2016 или Windows Server 2012.
manager: brianlic
ms.topic: article
ms.assetid: 88ffd598-2fde-402c-bd12-be790f84dc96
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 034a1738f67c452ba54cc0a1bf06a412120f2906
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101830995"
---
# <a name="plan-a-remote-access-cluster-deployment"></a>Планирование развертывания кластера удаленного доступа

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

 Windows Server 2016 и Windows Server 2012 объединяют VPN-подключение DirectAccess и службы удаленного доступа (RAS) к одной роли удаленного доступа. В этом обзоре приводятся общие сведения о шагах планирования, необходимых для развертывания кластера серверов удаленного доступа Windows Server 2016 или Windows Server 2012.

-   [Спланируйте расширенное развертывание DirectAccess](../../../directaccess/single-server-advanced/Plan-an-Advanced-DirectAccess-Deployment.md). Этот шаг включает планирование инфраструктуры, необходимой для развертывания одного сервера. Он включает в себя планирование параметров сети и сервера, требования к сертификатам, параметры DNS, развертывание сервера сетевого расположения, серверы управления DirectAccess, параметры Active Directory и объекты групповая политика (GPO).

-   [Шаг 2. Планирование серверов кластера](Step-2-Plan-Cluster-Servers.md) .

-   [Шаг 3. Планирование развертывания кластера Load-Balanced](Step-3-Plan-a-Load-Balanced-Cluster-Deployment.md).

-   Шаг 4. Запишите решения по планированию для расширенного развертывания удаленного доступа. Эти данные можно использовать как задание для всех лиц, участвующих в развертывании.

После завершения этих этапов планирования см. раздел [Настройка кластера удаленного доступа](../configure/Configure-a-Remote-Access-Cluster.md).

Инструкции по настройке развертывания кластера в качестве подтверждения концепции в лабораторной среде см. в статье [Тестовая лаборатория. демонстрация DirectAccess в кластере с Windows NLB](../../../directaccess/tlg-cluster-nlb/Test-Lab-Guide-Demonstrate-DirectAccess-in-a-Cluster-with-Windows-NLB.md).



