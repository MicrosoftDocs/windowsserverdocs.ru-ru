---
title: Управление доступом на основе ролей
description: Узнайте, как использовать управление доступом на основе ролей в IPAM.
manager: brianlic
ms.topic: article
ms.assetid: ecdfc589-fa14-4bb3-ab7e-456ebc719385
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: e2a22019ee68d98f8122c79ebe8146c898164f7f
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2021
ms.locfileid: "98039364"
---
# <a name="role-based-access-control"></a>Управление доступом на основе ролей

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе содержатся сведения об использовании управления доступом на основе ролей в IPAM.

> [!NOTE]
> Помимо этого раздела, в этом разделе доступна следующая документация по контролю доступа IPAM.
>
> -   [Контроль управления доступом на основе ролей с помощью диспетчера серверов](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)
> -   [Контроль управления доступом на основе ролей с помощью Windows PowerShell](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)

Управление доступом на основе ролей позволяет задавать привилегии доступа на различных уровнях, включая DNS-сервер, зону DNS и уровни записи ресурсов DNS.
С помощью управления доступом на основе ролей можно указать, кто имеет детальный контроль над операциями для создания, изменения и удаления различных типов записей ресурсов DNS.

Можно настроить контроль доступа, чтобы пользователи были ограничены следующими разрешениями.

-   Пользователи могут изменять только определенные записи ресурсов DNS.

-   Пользователи могут изменять записи ресурсов DNS определенного типа, например PTR или MX.

-   Пользователи могут изменять записи ресурсов DNS для конкретных зон.

## <a name="see-also"></a>См. также:
[Управление доступом на основе ролей с помощью Диспетчер сервера](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md) 
 [Управление доступом на основе ролей с помощью Windows PowerShell](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md) 
 [Управление IPAM](Manage-IPAM.md)



