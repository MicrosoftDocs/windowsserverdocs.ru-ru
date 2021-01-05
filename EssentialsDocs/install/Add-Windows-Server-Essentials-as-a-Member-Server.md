---
title: Добавление Windows Server Essentials в качестве рядового сервера
description: Узнайте, как добавить Windows Server Essentials в качестве рядового сервера в существующую доменную среду Active Directory.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: d09dd82f-f7d2-47ce-862d-fd9869f2021c
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 470d713d2d9b105c834369cd15dad372f843a67d
ms.sourcegitcommit: d2224cf55c5d4a653c18908da4becf94fb01819e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2020
ms.locfileid: "97711619"
---
# <a name="add-windows-server-essentials-as-a-member-server"></a>Добавление Windows Server Essentials в качестве рядового сервера

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Этот раздел относится к серверу под Windows Server 2012 R2 Standard, Windows Server 2012 R2 Datacenter или Windows Server 2016 с установленной ролью Windows Server Essentials Experience. В оставшейся части этого документа роль Windows Server Essentials Experience будет называться Windows Server Essentials.

> [!NOTE]
>   Windows Server Essentials можно развернуть только в качестве контроллера домена. В этом документе Windows Server Essentials не включает Windows Server Essentials.

 Windows Server Essentials необязательно быть основным сервером в домене Windows. Вы можете добавить Windows Server Essentials в качестве рядового сервера в существующую среду домена Active Directory и использовать все преимущества защиты данных, безопасного удаленного доступа и интеграции с облачными службами, которые он предоставляет. Кроме того, Windows Server Essentials можно развернуть в существующей среде Active Directory не только как контроллер домена. Это позволяет расширить хранилище или использовать филиал для локального хранения данных и администрирования.

 Windows Server Essentials можно добавить одним из следующих способов.

-   Добавьте Windows Server Essentials в филиал своего офиса и присоедините его к контроллеру домена, расположенному в главном офисе с помощью стандартных средств. Вы можете включить функцию BranchCache для использования оптимальной пропускной способности данного рядового сервера.

-   Добавьте Windows Server Essentials в качестве рядового сервера в сети Windows Server Essentials, чтобы расширить возможности хранения в сети путем добавления дополнительных серверных папок на рядовом сервере.

-   Добавьте Windows Server Essentials в качестве рядового сервера в локальном офисе, если основной сервер под управлением Windows Server Essentials размещен в Microsoft Azure или размещен сторонними поставщиками услуг размещения. Использование Windows Server Essentials в качестве рядового сервера в локальном офисе позволяет оптимизировать пропускную способность.

## <a name="adding-windows-server-essentials-as-a-member-server"></a>Добавление Windows Server Essentials в качестве рядового сервера
 Чтобы добавить Windows Server Essentials в качестве рядового сервера к основному серверу под Windows Server 2012 R2 или Windows Server Essentials в существующей Active Directory среде, необходимо выполнить следующие действия.

1.  Присоедините сервер под управлением Windows Server Essentials к рабочей группе.

2.  Присоедините сервер под Windows Server Essentials к домену основного сервера Windows Server Essentials.

3.  Настройте интерфейс Windows Server Essentials с диспетчер сервера.

#### <a name="to-join-windows-server-essentials-to-a-workgroup-or-domain"></a>Присоединение Windows Server Essentials к рабочей группе или домену

1. После завершения установки Windows Server Essentials на втором сервере закройте мастер настройки Windows Server Essentials.

2. В поле **Поиск** введите **System Settings** и в результатах поиска выберите **Просмотр расширенных параметров системы**.

3. В окне **Свойства системы** перейдите на вкладку **Имя компьютера**.

4. В окне **Имя компьютера** в разделе **Домен** нажмите кнопку **Изменить**.

5. В области **изменение имени компьютера или домена** в разделе **член** выберите, следует ли присоединить сервер под Windows Server Essentials к **рабочей группе** или **домену**.

   -   Чтобы добавить сервер к рабочей группе, введите команду **workgroup**, а затем нажмите кнопку **ОК**.

   -   Чтобы присоединить этот сервер к существующему домену Active Directory, введите имя домена и нажмите кнопку **ОК**.

6. Чтобы изменения вступили в силу, перезагрузите сервер.

   После присоединения сервера к домену основного сервера можно продолжить настройку Windows Server Essentials, запустив мастер настройки Windows Server Essentials из диспетчер сервера.

#### <a name="to-configure-windows-server-essentials-experience-on-a-member-server"></a>Настройка Windows Server Essentials Experience на рядовом сервере

1.  (Необязательно) При необходимости измените имя сервера.

    > [!IMPORTANT]
    >  После настройки интерфейса Windows Server Essentials изменить имя сервера невозможно.

2.  Войдите в сервер с помощью учетной записи администратора домена.

3.  Откройте диспетчер сервера.

4.  В области уведомлений в **диспетчере сервера** установите флажок, а затем выберите **Настройка Windows Server Essentials**.

5.  Выберите настройку сервера в качестве рядового сервера и нажмите кнопку **Далее**.

6.  Щелкните **Настройка**, чтобы приступить к настройке. Процесс настройки занимает около 10 минут.

7.  На рабочем столе щелкните значок панели мониторинга для запуска панели мониторинга. На домашней странице завершите задачи **Приступая к работе**, перечисленные на вкладке **Установка**.

## <a name="additional-references"></a>Дополнительные ссылки


-   [Установка Windows Server Essentials](Install-Windows-Server-Essentials.md)

-   [Установка Windows Server Essentials](../install/Install-Windows-Server-Essentials.md)

