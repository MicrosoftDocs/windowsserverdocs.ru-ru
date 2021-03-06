---
title: Просмотр записей ресурсов DNS для зоны DNS
description: Узнайте, как просматривать записи ресурсов DNS для зоны DNS в консоли клиента IPAM.
manager: brianlic
ms.topic: article
ms.assetid: 375feefc-949e-47c3-9e61-35b79e021966
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: d1d7193855e4476fe84f915d9cc1cd487b37f3be
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101829989"
---
# <a name="view-dns-resource-records-for-a-dns-zone"></a>Просмотр записей ресурсов DNS для зоны DNS

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Этот раздел можно использовать для просмотра записей ресурсов DNS для зоны DNS в консоли клиента IPAM.

Для выполнения этой процедуры необходимо быть членом группы **Администраторы** или пользователем с аналогичными правами.

### <a name="to-view-dns-resource-records-for-a-zone"></a>Просмотр записей ресурсов DNS для зоны

1.  В диспетчер сервера щелкните  **IPAM**. Откроется консоль клиента IPAM.

2.  В области навигации в окне **мониторинг и управление** щелкните **зоны DNS**.  Панель навигации разделяется на верхнюю панель навигации и нижнюю панель навигации.

3.  В нижней области навигации щелкните **прямой поиск**, а затем разверните список домены и зона, чтобы найти и выбрать зону, которую нужно просмотреть. Например, если имеется зона с именем Dublin, щелкните элемент **Dublin**.

    ![Выберите зону, которую нужно просмотреть](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01a.jpg)


4.  В области отображения представлением по умолчанию являются DNS-серверы для зоны. Чтобы изменить представление, щелкните **Текущее представление**, а затем — **записи ресурсов**.

    ![Изменение представления на записи ресурсов](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_Zone_RR_02.jpg)

5.  Отобразятся записи ресурсов DNS для зоны. Чтобы отфильтровать записи, введите текст, который нужно найти в поле **Фильтр**.

    ![Введите текст для фильтрации записей](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01c.jpg)

6.  Чтобы отфильтровать записи ресурсов по типу записи, области доступа или другим критериям, нажмите кнопку **Добавить условие**, а затем выберите в списке критерий и нажмите кнопку **Добавить**.

    ![Использование критериев для фильтрации записей](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01d.jpg)

## <a name="see-also"></a>См. также:
[Управление](DNS-Zone-Management.md) 
 зоной DNS [Управление IPAM](Manage-IPAM.md)



