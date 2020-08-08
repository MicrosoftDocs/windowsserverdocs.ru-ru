---
title: Настройка пространств имен DFS
description: В этой статье рассматривается, как проводить тонкую настройку или оптимизацию пространств имен DFS.
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 348a34e24cf7d22dc376df37607f21f1dceea74a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939400"
---
# <a name="tuning-dfs-namespaces"></a>Настройка пространств имен DFS

> Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

После создания пространства имен и добавления папок и конечных объектов обратитесь к следующим разделам, чтобы настроить или оптимизировать то, как пространство имен DFS обрабатывает ссылки и опрашивает доменные службы Active Directory (AD DS) для получения актуальных данных пространства имен:

-   [Включение перечисления на основе доступа в пространстве имен](enable-access-based-enumeration-on-a-namespace.md)
-   [Включение и отключение ссылок и восстановление размещения клиента](enable-or-disable-referrals-and-client-failback.md)
-   [Изменение времени, в течение которого клиенты кэшируют ссылки](change-the-amount-of-time-that-clients-cache-referrals.md)
-   [Задание метода сортировки конечных объектов в ссылках](set-the-ordering-method-for-targets-in-referrals.md)
-   [Задание приоритета конечных объектов для переопределения порядка в ссылках](set-target-priority-to-override-referral-ordering.md)
-   [Оптимизация опроса пространства имен](optimize-namespace-polling.md)
-   [Использование наследуемых разрешений с перечислением на основе доступа](using-inherited-permissions-with-access-based-enumeration.md)

> [!NOTE]
> Для поиска папок или конечных объектов папок выберите пространство имен, перейдите на вкладку **Поиск**, введите строку поиска в текстовом поле и нажмите кнопку **Поиск**.