---
title: Удаление записей ресурсов DNS
description: Этот раздел является частью руководства по управлению IP-адресами (IPAM) в Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 366e6fd5-d563-4de3-9551-5614cbb8f2cb
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8c93af6a5d43086320ab27982f7a0c0308ee551d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312462"
---
# <a name="delete-dns-resource-records"></a>Удаление записей ресурсов DNS

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016

Этот раздел можно использовать для удаления одной или нескольких записей ресурсов DNS с помощью консоли клиента IPAM.  
  
Для выполнения этой процедуры необходимо быть членом группы **Администраторы** или пользователем с аналогичными правами.  
  
### <a name="to-delete-dns-resource-records"></a>Удаление записей ресурсов DNS  
  
1.  В диспетчер сервера щелкните **IPAM**. Откроется консоль клиента IPAM.  
  
2.  В области навигации в окне **мониторинг и управление**щелкните **зоны DNS**.  Панель навигации разделяется на верхнюю панель навигации и нижнюю панель навигации.  
  
3.  Щелкните, чтобы развернуть « **прямой просмотр** » и домен, в котором находятся записи зоны и ресурса, которые необходимо удалить. Щелкните зону и на панели отображения щелкните **Текущее представление**. Щелкните **записи ресурсов**.  
  
4.  На панели "дисплей" выберите записи ресурсов, которые необходимо удалить.  
  
    ![Выберите записи ресурсов для удаления](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_01.jpg)  
  
5.  Щелкните правой кнопкой мыши выбранные записи и выберите пункт **Удалить запись ресурса DNS**.  
  
    ![Удаление записей](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_02.jpg)  
  
6.  Откроется диалоговое окно **Удаление записи ресурса DNS** . Убедитесь, что выбран правильный DNS-сервер. Если это не так, щелкните **DNS-сервер** и выберите сервер, с которого нужно удалить записи ресурсов. Нажмите кнопку **ОК**. IPAM удаляет записи ресурсов с DNS-сервера.  
  
    ![Убедитесь, что выбран правильный DNS-сервер, и удалите записи.](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_03.jpg)  
  
## <a name="see-also"></a>См. также  
[Управление записью ресурса DNS](DNS-Resource-Record-Management.md)  
[Управление IPAM](Manage-IPAM.md)  
  


