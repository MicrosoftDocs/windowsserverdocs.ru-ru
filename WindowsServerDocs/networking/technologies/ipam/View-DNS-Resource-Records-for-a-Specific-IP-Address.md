---
title: Просмотр записей ресурсов DNS для определенного IP-адреса
description: Этот раздел является частью руководства по управлению IP-адресами (IPAM) в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: f590fb86-4195-4f90-98cb-e90459d4c1e3
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 2f1dd1f87ecaa390d5e5c43a7dc2ad9267fe8161
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948320"
---
# <a name="view-dns-resource-records-for-a-specific-ip-address"></a>Просмотр записей ресурсов DNS для определенного IP-адреса

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

С помощью этого раздела можно просмотреть записи ресурсов DNS, связанные с выбранным IP-адресом.

Для выполнения этой процедуры необходимо быть членом группы **Администраторы** или пользователем с аналогичными правами.

### <a name="to-view-resource-records-for-an-ip-address"></a>Просмотр записей ресурсов для IP-адреса

1.  В диспетчер сервера щелкните  **IPAM**. Откроется консоль клиента IPAM.

2.  В области навигации в **поле IP-адрес** выберите пункт **Инвентаризация IP-адресов**. В нижней области навигации щелкните **IPv4** или **IPv6**. Инвентаризация IP-адресов отображается в представлении поиска панели отображения. Выберите IP-адрес, записи ресурсов DNS которого необходимо просмотреть.

    ![Просмотр перечня IP-адресов](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_01.jpg)

3.  В **представлении сведения о** панели отображения щелкните **записи ресурсов DNS**. Отобразятся записи ресурсов, связанные с выбранным IP-адресом.

    ![Просмотр записей ресурсов DNS](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_02.jpg)

## <a name="see-also"></a>См. также:
Управление записью [ресурса DNS](DNS-Resource-Record-Management.md) 
 [Управление IPAM](Manage-IPAM.md)



