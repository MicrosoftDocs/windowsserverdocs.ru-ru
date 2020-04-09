---
title: Планирование развертывания кластера удаленного доступа
description: Этот раздел является частью руководств по развертыванию удаленного доступа в кластере в Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 88ffd598-2fde-402c-bd12-be790f84dc96
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9a3bf30f6de6472fdd67748a3a387eaa2068d5c4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855257"
---
# <a name="plan-a-remote-access-cluster-deployment"></a>Планирование развертывания кластера удаленного доступа

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016

 Windows Server 2016 и Windows Server 2012 объединяют VPN-подключение DirectAccess и службы удаленного доступа (RAS) к одной роли удаленного доступа. В этом обзоре приводятся общие сведения о шагах планирования, необходимых для развертывания кластера серверов удаленного доступа Windows Server 2016 или Windows Server 2012.
  
-   [Спланируйте расширенное развертывание DirectAccess](../../../directaccess/single-server-advanced/Plan-an-Advanced-DirectAccess-Deployment.md). Этот шаг включает планирование инфраструктуры, необходимой для развертывания одного сервера. Он включает в себя планирование параметров сети и сервера, требования к сертификатам, параметры DNS, развертывание сервера сетевого расположения, серверы управления DirectAccess, параметры Active Directory и объекты групповая политика (GPO).  
  
-   [Шаг 2. Планирование серверов кластера](Step-2-Plan-Cluster-Servers.md) .  
  
-   [Шаг 3. Планирование развертывания кластера с балансировкой нагрузки](Step-3-Plan-a-Load-Balanced-Cluster-Deployment.md).  
  
-   Шаг 4. Запишите решения по планированию для расширенного развертывания удаленного доступа. Эти данные можно использовать как задание для всех лиц, участвующих в развертывании.  
  
После завершения этих этапов планирования см. раздел [Настройка кластера удаленного доступа](../configure/Configure-a-Remote-Access-Cluster.md). 

Инструкции по настройке развертывания кластера в качестве подтверждения концепции в лабораторной среде см. в статье [Тестовая лаборатория. демонстрация DirectAccess в кластере с Windows NLB](../../../directaccess/tlg-cluster-nlb/Test-Lab-Guide-Demonstrate-DirectAccess-in-a-Cluster-with-Windows-NLB.md).  
  


