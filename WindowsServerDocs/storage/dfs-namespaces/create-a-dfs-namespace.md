---
title: Создание пространства имен DFS
description: В этой статье рассматривается, как создать пространство имен DFS.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 60b31b90ed54137898043e79c3c6504afb3f4b7f
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2020
ms.locfileid: "86953366"
---
# <a name="create-a-dfs-namespace"></a>Создание пространства имен DFS

> Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Чтобы создать новое пространство имен, можно использовать диспетчер сервера для создания пространства имен при установке службы роли "Пространства имен DFS". Также можно использовать [командлет New-DfsnRoot](/powershell/module/dfsn/new-dfsnroot) из сеанса Windows PowerShell.

Модуль DFSN Windows PowerShell был введен в Windows Server 2012.

Другой вариант — использовать следующую процедуру для создания пространства имен после установки службы роли.

## <a name="to-create-a-namespace"></a>Создание пространства имен

1.  Нажмите кнопку **Пуск**, укажите пункт **Администрирование**, а затем щелкните **Управление DFS**.

2.  В дереве консоли щелкните правой кнопкой мыши узел **Пространства имен** и выберите **Новое пространство имен**.

3.  Следуйте инструкциям в **Мастере создания нового пространства имен**.

    Чтобы создать изолированное пространство имен в отказоустойчивом кластере, укажите имя экземпляра кластерного файлового сервера на странице **Сервер пространства имен** в **Мастере создания нового пространства имен**.

> [!IMPORTANT]
> Не пытайтесь создавать доменное пространство имен с использованием режима Windows Server 2008, если режим работы леса — Windows Server 2003 или выше. В противном случае вы получите пространство имен, в котором не сможете удалять папки DFS. Будет появляться следующее сообщение об ошибке: "Невозможно удалить папку. Не удается завершить выполнение функции".

## <a name="additional-references"></a>Дополнительные ссылки

-   [Развертывание пространств имен DFS](deploying-dfs-namespaces.md)
-   [Выбор типа пространства имен](choose-a-namespace-type.md)
-   [Добавление серверов пространств имен в доменное пространство имен DFS](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   [Делегирование разрешений на управление для пространств имен DFS](delegate-management-permissions-for-dfs-namespaces.md).
