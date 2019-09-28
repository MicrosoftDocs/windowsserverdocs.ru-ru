---
title: Новые возможности DNS-клиента в Windows Server
description: В этом разделе приводятся общие сведения о новых возможностях DNS-клиента в Windows Server и Windows 10.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: 6edaba84-4595-4fd8-95d7-64d4d975a38a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 696ea0b499a4132d630cc0cda15a1d7efdac37a8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356060"
---
# <a name="whats-new-in-dns-client-in-windows-server-2016"></a>Новые возможности DNS-клиента в Windows Server 2016

>Относится к: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе описываются функциональные возможности клиента службы доменных имен (DNS), новые или измененные в Windows 10 и Windows Server 2016 и более поздних версиях этих операционных систем.
  
## <a name="updates-to-dns-client"></a>Обновления DNS-клиента

**Привязка службы клиента DNS**: В Windows 10 служба DNS-клиента обеспечивает расширенную поддержку компьютеров с несколькими сетевыми интерфейсами. Для многосетевых компьютеров разрешение DNS оптимизируется следующими способами.  
  
-   Когда DNS-сервер, настроенный на определенном интерфейсе, используется для разрешения DNS-запроса, служба DNS-клиента будет привязана к этому интерфейсу перед отправкой запроса DNS.  
  
    При привязке к определенному интерфейсу DNS-клиент может четко указать интерфейс, где происходит разрешение имен, что позволяет приложениям оптимизировать взаимодействие с DNS-клиентом через этот сетевой интерфейс.  
  
-   Если используемый DNS-сервер назначен параметром групповая политика из таблица политики разрешения имен (NRPT), то служба DNS-клиента не привязывается к конкретному интерфейсу.  
  
> [!NOTE]  
> Изменения в службе DNS-клиента в Windows 10 также существуют на компьютерах под управлением Windows Server 2016 и более поздних версий.  
  
## <a name="see-also"></a>См. также  
  
-   [Новые возможности DNS-сервера в Windows Server 2016](What-s-New-in-DNS-Server.md)  
  

