---
title: Планирование многосайтового развертывания
description: Эта статья является частью руководств по развертыванию нескольких серверов удаленного доступа в многосайтовом развертывании в Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8387eabe-7363-4367-b5b1-03c67baa2933
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d5c189969c31ef9627dd7daee0e09162ea9aec39
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313872"
---
# <a name="plan-a-multisite-deployment"></a>Планирование многосайтового развертывания

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016

 Windows Server 2016, Windows Server 2012 объединяют VPN DirectAccess и службы маршрутизации и удаленного доступа (RRAS) в одну роль удаленного доступа. Этот обзор содержит вводные сведения о шагах планирования, необходимых для развертывания удаленного доступа Windows Server 2016 или Windows Server 2012 в многосайтовой конфигурации.  
  
1.  [Разверните один сервер DirectAccess с дополнительными параметрами](https://technet.microsoft.com/library/hh831436(v=ws.11).aspx). Этот шаг включает планирование инфраструктуры, необходимой для развертывания одного сервера. Он включает в себя планирование параметров сети и сервера, требования к сертификатам, параметры DNS, развертывание сервера сетевого расположения, серверы управления DirectAccess, параметры Active Directory и объекты групповая политика (GPO).  
  
2.  [Шаг 2. Планирование многосайтовой инфраструктуры](Step-2-Plan-the-Multisite-Infrastructure.md). Этот шаг включает в себя Active Directory и планирование объектов групповой политики, а также конфигурацию DNS.  
  
3.  [Шаг 3. Планирование многосайтового развертывания](Step-3-Plan-the-Multisite-Deployment.md). Этот шаг включает в себя планирование параметров сертификата, конфигурации сервера сетевого расположения, параметров точки входа клиента, параметров префикса IPv6 и необязательных параметров глобальной балансировки нагрузки.  
  
> [!NOTE]  
> Запишите решения по планированию для расширенного развертывания удаленного доступа. Эти данные можно использовать как задание для всех лиц, участвующих в развертывании.  
  
После завершения этих этапов планирования см. раздел [Настройка многосайтового развертывания](../configure/Configure-a-Multisite-Deployment.md).  
  


