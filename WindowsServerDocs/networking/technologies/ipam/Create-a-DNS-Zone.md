---
title: Создание зоны DNS
description: Узнайте, как создать зону DNS с помощью консоли клиента IPAM.
manager: brianlic
ms.topic: article
ms.assetid: a030ff51-a815-4fc4-b26d-aae41c3e4ce5
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 04e1e393a5f434ae171ed25da4324955bea4e595
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2021
ms.locfileid: "98039694"
---
# <a name="create-a-dns-zone"></a>Создание зоны DNS

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

С помощью этого раздела можно создать зону DNS с помощью консоли клиента IPAM.

Для выполнения этой процедуры необходимо быть членом группы **Администраторы** или пользователем с аналогичными правами.

### <a name="to-create-a-dns-zone"></a>Создание зоны DNS

1.  В диспетчер сервера щелкните  **IPAM**. Откроется консоль клиента IPAM.

2.  В области навигации в окне **мониторинг и управление** щелкните **DNS и DHCP-серверы**. На панели "дисплей" выберите **Тип сервера**, а затем щелкните **DNS**. Все DNS-серверы, управляемые IPAM, перечислены в результатах поиска.

3.  Выберите сервер, на который нужно добавить зону, и щелкните правой кнопкой мыши сервер.  Щелкните **создать зону DNS**.

    ![Создание зоны DNS](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_01a.jpg)

4.  Откроется диалоговое окно **Создание зоны DNS** . В окне **Общие свойства** выберите категорию зоны, тип зоны и введите имя в списке **имя зоны**. Также выберите значения, подходящие для развертывания, в окне **Дополнительные свойства** и нажмите кнопку **ОК**.

    ![Дополнительные свойства](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_02a.jpg)

## <a name="see-also"></a>См. также:
[Управление](DNS-Zone-Management.md) 
 зоной DNS [Управление IPAM](Manage-IPAM.md)



