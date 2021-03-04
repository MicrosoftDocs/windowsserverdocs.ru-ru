---
title: Задание области доступа для зоны DNS
description: Узнайте, как задать область доступа для зоны DNS с помощью консоли клиента IPAM.
manager: brianlic
ms.topic: article
ms.assetid: 6a211dde-80eb-4888-b5bb-4e28fe8dc7df
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: e89fe6fb6748dd7efeb29d83bfdbf6d5e0620526
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101829979"
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



