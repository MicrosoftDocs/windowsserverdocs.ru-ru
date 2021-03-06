---
title: Задание области доступа для записей ресурсов DNS
description: Узнайте, как задать область доступа для записей ресурсов DNS с помощью консоли клиента IPAM.
manager: brianlic
ms.topic: article
ms.assetid: a96a8752-5678-49c5-b069-d2cce8042a51
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 8ce54beb23082877228309b6aeb6b9bda28e4c80
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101829999"
---
# <a name="set-access-scope-for-dns-resource-records"></a>Задание области доступа для записей ресурсов DNS

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Этот раздел можно использовать для задания области доступа для записей ресурсов DNS с помощью консоли клиента IPAM.

Для выполнения этой процедуры необходимо быть членом группы **Администраторы** или пользователем с аналогичными правами.

### <a name="to-set-access-scope-for-dns-resource-records"></a>Настройка области доступа для записей ресурсов DNS

1.  В диспетчер сервера щелкните  **IPAM**. Откроется консоль клиента IPAM.

2.  В области навигации щелкните **зоны DNS**.  В нижней области навигации разверните узел **прямой просмотр** и выберите зону, содержащую записи ресурсов, область доступа которой требуется изменить.

3.  На панели "дисплей" выберите записи ресурсов, область доступа к которой необходимо изменить.

    ![Выбор записей ресурсов](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_02.jpg)

4.  Щелкните правой кнопкой мыши выбранные записи ресурсов DNS и выберите **задать область доступа**.

    ![Задание области доступа](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_03.jpg)

5.  Откроется диалоговое окно **Установка области доступа** . Если требуется для развертывания, щелкните, чтобы снять флажок **наследовать область доступа от родительского объекта**. В **области выберите область доступа** выберите элемент и нажмите кнопку **ОК**.

    ![Выберите область доступа](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_04.jpg)

## <a name="see-also"></a>См. также:
Управление доступом на [основе ролей](Role-based-Access-Control.md) 
 [Управление IPAM](Manage-IPAM.md)



