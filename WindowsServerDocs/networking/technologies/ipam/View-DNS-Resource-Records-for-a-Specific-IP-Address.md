---
title: Просмотр записей ресурсов DNS для определенного IP-адреса
description: Этот раздел является частью руководства по управлению IP-адресами (IPAM) в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: f590fb86-4195-4f90-98cb-e90459d4c1e3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 211dcfdc17cfa81aad7adb1a424a9fadc0c932c6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944605"
---
# <a name="view-dns-resource-records-for-a-specific-ip-address"></a>Просмотр записей ресурсов DNS для определенного IP-адреса

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

С помощью этого раздела можно просмотреть записи ресурсов DNS, связанные с выбранным IP-адресом.

Для выполнения этой процедуры необходимо быть членом группы **Администраторы** или пользователем с аналогичными правами.

### <a name="to-view-resource-records-for-an-ip-address"></a>Просмотр записей ресурсов для IP-адреса

1.  В диспетчер сервера щелкните **IPAM**. Откроется консоль клиента IPAM.

2.  В области навигации в **поле IP-адрес**выберите пункт **Инвентаризация IP-адресов**. В нижней области навигации щелкните **IPv4** или **IPv6**. Инвентаризация IP-адресов отображается в представлении поиска панели отображения. Выберите IP-адрес, записи ресурсов DNS которого необходимо просмотреть.

    ![Просмотр перечня IP-адресов](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_01.jpg)

3.  В **представлении сведения о**панели отображения щелкните **записи ресурсов DNS**. Отобразятся записи ресурсов, связанные с выбранным IP-адресом.

    ![Просмотр записей ресурсов DNS](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_02.jpg)

## <a name="see-also"></a>См. также:
Управление записью [ресурса DNS](DNS-Resource-Record-Management.md) 
 [Управление IPAM](Manage-IPAM.md)



