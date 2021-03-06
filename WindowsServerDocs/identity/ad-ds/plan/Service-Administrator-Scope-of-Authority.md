---
description: 'Дополнительные сведения: область полномочий администратора службы'
ms.assetid: da7b6dcf-53ec-4394-88c0-c087d92f3893
title: Объем полномочий администратора службы
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 600ee3ff18464219f278b1525db6e3a14e5ab1f3
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049282"
---
# <a name="service-administrator-scope-of-authority"></a>Объем полномочий администратора службы

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Если вы решили участвовать в Active Directory лесу, необходимо доверять владельцу леса и администраторам служб. Владельцы леса отвечают за выбор и Управление администраторами служб. Таким образом, если вы доверяете владельцу леса, вы также доверяете администраторам служб, которыми управляет владелец леса. Эти администраторы служб имеют доступ ко всем ресурсам в лесу. Прежде чем принимать решение принять участие в лесу, важно понимать, что владелец леса и администраторы служб получат полный доступ к данным. Этот доступ нельзя запретить.

Все администраторы служб в лесу имеют полный контроль над всеми данными и службами на всех компьютерах в лесу. Администраторы служб имеют возможность выполнять следующие действия.

-   Исправьте ошибки в списках управления доступом (ACL) объектов. Это позволяет администратору службы читать, изменять или удалять объекты независимо от списков управления доступом, установленных для этих объектов.

-   Измените системное по на контроллере домена, чтобы обойти обычные проверки безопасности. Это позволяет администратору службы просматривать или манипулировать любыми объектами в домене независимо от списка ACL в объекте.

-   Используйте политику безопасности группы с ограниченным доступом для предоставления любому пользователю или группе административного доступа к любому компьютеру, присоединенному к домену. Таким образом администраторы служб могут получить контроль над любым компьютером, присоединенным к домену, независимо от намерения владельца компьютера.

-   Сброс паролей или изменение членства в группах для пользователей.

-   Получите доступ к другим доменам в лесу, изменив системное программное обеспечение на контроллере домена. Администраторы служб могут повлиять на работу любого домена в лесу, просматривать данные конфигурации леса или управлять ими, просматривать данные, хранящиеся в любом домене, а также управлять данными, хранящимися на любом компьютере, присоединенном к лесу.

По этой причине группы, которые хранят данные в подразделениях (OU) в лесу и присоединяются компьютеры к лесу, должны доверять администраторам служб. Чтобы группа присоединиться к лесу, необходимо выбрать доверие всем администраторам служб в лесу. Это включает в себя следующие гарантии:

-   Владелец леса может быть доверенным, чтобы действовать в интересах группы, и не имеет причины для злонамеренного действия с группой.

-   Владелец леса соответствующим образом ограничит физический доступ к контроллерам домена. Контроллеры домена в лесу не могут быть изолированы друг от друга. Злоумышленник, имеющий физический доступ к одному контроллеру домена, может вносить изменения в базу данных каталогов в автономном режиме и, таким образом, конфликтует с работой любого домена в лесу, просматривать или обрабатывать данные, хранящиеся в любом месте леса, просматривать или обрабатывать данные, хранящиеся на любом компьютере, присоединенном к лесу. По этой причине физический доступ к контроллерам домена должен быть ограничен доверенным персоналом.

-   Вы понимаете и принимаете потенциальный риск, что администраторы доверенных служб могут привести к ослаблению безопасности системы.

Некоторые группы могут определить, что преимущества совместной работы и экономии ресурсов, участвующие в общей инфраструктуре, перевешивают риски, которые администраторы служб будут использовать или будут приводить к неправильному использованию. Эти группы могут предоставлять общий доступ к лесу и использовать подразделения для делегирования полномочий. Однако другие группы могут не принять этот риск, так как последствия компрометации безопасности слишком серьезны. Для этих групп требуются отдельные леса.



