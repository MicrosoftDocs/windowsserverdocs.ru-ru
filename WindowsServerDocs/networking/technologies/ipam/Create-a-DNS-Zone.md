---
title: Создание зоны DNS
description: Этот раздел является частью руководства по управлению IP-адресами (IPAM) в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: a030ff51-a815-4fc4-b26d-aae41c3e4ce5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0635c91b3dd61db6df41c2836cc5efc65d9de520
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970791"
---
# <a name="create-a-dns-zone"></a>Создание зоны DNS

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

С помощью этого раздела можно создать зону DNS с помощью консоли клиента IPAM.

Для выполнения этой процедуры необходимо быть членом группы **Администраторы** или пользователем с аналогичными правами.

### <a name="to-create-a-dns-zone"></a>Создание зоны DNS

1.  В диспетчер сервера щелкните **IPAM**. Откроется консоль клиента IPAM.

2.  В области навигации в окне **мониторинг и управление**щелкните **DNS и DHCP-серверы**. На панели "дисплей" выберите **Тип сервера**, а затем щелкните **DNS**. Все DNS-серверы, управляемые IPAM, перечислены в результатах поиска.

3.  Выберите сервер, на который нужно добавить зону, и щелкните правой кнопкой мыши сервер.  Щелкните **создать зону DNS**.

    ![Создание зоны DNS](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_01a.jpg)

4.  Откроется диалоговое окно **Создание зоны DNS** . В окне **Общие свойства**выберите категорию зоны, тип зоны и введите имя в списке **имя зоны**. Также выберите значения, подходящие для развертывания, в окне **Дополнительные свойства**и нажмите кнопку **ОК**.

    ![Дополнительные свойства](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_02a.jpg)

## <a name="see-also"></a>См. также:
[Управление](DNS-Zone-Management.md) 
 зоной DNS [Управление IPAM](Manage-IPAM.md)



