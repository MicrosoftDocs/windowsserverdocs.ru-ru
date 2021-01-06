---
title: Создание роли пользователя для управления доступом
description: Этот раздел является частью руководства по управлению IP-адресами (IPAM) в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: ae6a42db-a104-401b-a8e6-b85c47d30b46
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: fc0f0adbc19841662b8ec95491196c8047bd0cc2
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948040"
---
# <a name="create-a-user-role-for-access-control"></a>Создание роли пользователя для управления доступом

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

С помощью этого раздела можно создать новую роль пользователя "Управление доступом" в консоли клиента IPAM.

Для выполнения этой процедуры необходимо быть членом группы **Администраторы** или пользователем с аналогичными правами.

> [!NOTE]
> После создания роли можно создать политику доступа для назначения роли конкретному пользователю или группе Active Directory. Дополнительные сведения см. в разделе [Создание политики доступа](../../technologies/ipam/Create-an-Access-Policy.md).

### <a name="to-create-a-role"></a>Создание роли

1.  В диспетчер сервера щелкните  **IPAM**. Откроется консоль клиента IPAM.

2.  В области навигации щелкните **Управление доступом**, а затем в нижней области навигации щелкните **роли**.

    ![Роли контроля доступа](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_01.jpg)

3.  Щелкните правой кнопкой мыши элемент **роли** и выберите команду **Добавить роль пользователя**.

    ![Добавить роль пользователя](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_02.jpg)

4.  Откроется диалоговое окно **Добавление или изменение роли** . В поле **имя** введите имя роли, которая делает функцию роли понятной. Например, если вы хотите создать роль, которая позволяет администраторам управлять записями ресурсов SRV DNS, можно задать имя роли **ипамсрв**. При необходимости прокрутите список **операций** , чтобы определить тип операций, которые необходимо задать для роли. В этом примере прокрутите вниз до пункта **операции управления записями ресурсов DNS**.

    ![Операции управления записями ресурсов DNS](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_03.jpg)

5.  Разверните узел **операции управления записями ресурсов DNS**, а затем найдите **операции записи SRV**.

    ![Операции записи SRV](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_04.jpg)

6.  Разверните и выберите **операции записи SRV**, а затем нажмите кнопку **ОК**.

    ![Выбор операций записи SRV](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_05.jpg)

7.  В консоли клиента IPAM щелкните только что созданную роль. В **представлении Details** отображаются разрешенные операции для роли.

    ![Сведения о новой роли](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_06.jpg)

## <a name="see-also"></a>См. также:
Управление доступом на [основе ролей](Role-based-Access-Control.md) 
 [Управление IPAM](Manage-IPAM.md)



