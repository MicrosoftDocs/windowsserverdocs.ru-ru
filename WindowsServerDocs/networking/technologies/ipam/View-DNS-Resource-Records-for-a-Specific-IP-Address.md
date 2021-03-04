---
title: Просмотр записей ресурсов DNS для определенного IP-адреса
description: Узнайте, как просмотреть записи ресурсов DNS, связанные с выбранным IP-адресом.
manager: brianlic
ms.topic: article
ms.assetid: f590fb86-4195-4f90-98cb-e90459d4c1e3
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: c190df0fa5ae3263b8f00373d3e4d1eb9c81115f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101829969"
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



