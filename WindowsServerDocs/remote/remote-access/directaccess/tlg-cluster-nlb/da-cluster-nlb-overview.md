---
title: Обзор сценария лаборатории тестирования DirectAccess Cluster-NLB
description: Этот раздел входит руководство по лаборатории тестирования — продемонстрировать DirectAccess в кластере с помощью Windows NLB для Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd1e9efd-19e9-49e7-8432-881f661c9792
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 118a07b761979d3c32a8f7cf4f149aed56a1a893
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863585"
---
# <a name="overview-of-the-directaccess-cluster-nlb-test-lab-scenario"></a>Обзор сценария лаборатории тестирования DirectAccess Cluster-NLB

>Область применения. Windows Server (полугодовой канал), Windows Server 2016

В этом сценарии лаборатории тестирования DirectAccess развертывается с помощью:  
  
-   **DC1**- сервере, настроенном в качестве контроллера домена, сервера доменных имен (DNS) и сервера конфигурации протокола DHCP (Dynamic Host).  
  
-   **EDGE1**- серверу во внутренней сети, настроенный в качестве первого сервера удаленного доступа в кластере серверов удаленного доступа. У этого сервера два сетевых адаптера; один из которых подключен к внутренней сети, а второй к внешней сети.  
  
-   **EDGE2**- серверу во внутренней сети, настроенный в качестве второго сервера удаленного доступа в кластере серверов удаленного доступа. У этого сервера два сетевых адаптера; один из которых подключен к внутренней сети, а второй к внешней сети.  
  
-   **App1**- серверу во внутренней сети, настроенный как сервер веб-приложений и файлов, а также как корневого центра сертификации (ЦС) предприятия  
  
-   **APP2**— компьютер во внутренней сети, настроенный в качестве IPv4 только веб- и файловым сервером. Этот компьютер используется для описания возможностей NAT64/DNS64.  
  
-   **INET1**- сервере, настроенном в качестве Internet DNS и DHCP-сервера.  
  
-   **NAT1**- клиентский компьютер, настроенный в качестве сетевого адреса translator (NAT) устройства с помощью подключения к Интернету.  
  
-   **CLIENT1**- клиент, настроенный в качестве клиента DirectAccess, который будет использоваться для проверки подключения DirectAccess при перемещении между внутренней сети, смоделированной сети Интернет и домашней сети.  
  
Лаборатория тестирования включает три подсети, которые имитируют следующее:  
  
-   Домашняя сеть с именем Homenet (192.168.137.0/24) подключен к Интернету, NAT.  
  
-   Внешние сети, представленного подсети Интернет (131.107.0.0/24).  
  
-   Внутренняя сеть с именем Corpnet (10.0.0.0/24; 2001:db8:1:: / 64) отделены от Интернета, сервер удаленного доступа.  
  
Компьютеры в каждой подсети подключаются, с помощью физических или виртуальных концентратора или коммутатора, как показано на рисунке ниже.  
  
![Обзор лаборатории тестирования](../../../media/Overview-of-the-Test-Lab-Scenario_5/TLG_DA_Cluster.png)  
  

