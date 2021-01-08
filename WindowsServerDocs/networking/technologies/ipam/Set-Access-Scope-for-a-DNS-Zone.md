---
title: Задание области доступа для зоны DNS
description: Узнайте, как задать область доступа для зоны DNS с помощью консоли клиента IPAM.
manager: brianlic
ms.topic: article
ms.assetid: 6a211dde-80eb-4888-b5bb-4e28fe8dc7df
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 8d679dcc0e16e1dc3e38e11247637463a26ed0f5
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2021
ms.locfileid: "98040144"
---
# <a name="set-access-scope-for-a-dns-zone"></a>Задание области доступа для зоны DNS

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Этот раздел можно использовать для задания области доступа для зоны DNS с помощью консоли клиента IPAM.

Для выполнения этой процедуры необходимо быть членом группы **Администраторы** или пользователем с аналогичными правами.

### <a name="to-set-the-access-scope-for-a-dns-zone"></a>Настройка области доступа для зоны DNS

1.  В диспетчер сервера щелкните  **IPAM**. Откроется консоль клиента IPAM.

2.  В области навигации щелкните **зоны DNS**. На панели "дисплей" щелкните правой кнопкой мыши зону DNS, для которой необходимо изменить область доступа, и выберите пункт **задать область доступа**.

    ![Задание области доступа](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_02.jpg)

3.  Откроется диалоговое окно **Установка области доступа** . Если требуется для развертывания, щелкните, чтобы снять флажок **наследовать область доступа от родительского объекта**. В **области выберите область доступа** выберите элемент и нажмите кнопку **ОК**.

    ![Выберите область доступа](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_03.jpg)

4.  В области отображение консоли клиента IPAM убедитесь, что область доступа для зоны изменилась.

    ![Убедитесь, что область доступа для зоны изменена.](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_04.jpg)

## <a name="see-also"></a>См. также:
Управление доступом на [основе ролей](Role-based-Access-Control.md) 
 [Управление IPAM](Manage-IPAM.md)



