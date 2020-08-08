---
title: Создание папки в пространстве имен DFS
description: В этой статье рассматривается, как папку в пространстве имен DFS.
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: d854cfcb02288f6262ee380edc0614baf9e29878
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957702"
---
# <a name="create-a-folder-in-a-dfs-namespace"></a>Создание папки в пространстве имен DFS

> Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Папки можно использовать для создания дополнительных уровней иерархии в пространстве имен. Можно также создавать папки с конечными объектами папок, чтобы добавлять в пространство имен общие папки. Папки DFS с конечными объектами папок не могут содержать другие папки DFS, поэтому, если вы хотите добавить в пространство имен уровень иерархии, не добавляйте в папку конечные объекты папки.

Выполните следующие действия, чтобы создать папку в пространстве имен с помощью оснастки "Управление DFS":

## <a name="to-create-a-folder-in-a-dfs-namespace"></a>Создание папки в пространстве имен DFS

1.  Нажмите кнопку **Пуск**, укажите пункт **Администрирование**, а затем щелкните **Управление DFS**.

2.  В узле **Пространства имен** дерева консоли щелкните правой кнопкой мыши пространство имен или папку внутри пространства имен и выберите **Новая папка**.

3.  В текстовом поле **Имя** введите имя новой папки.

4.  Чтобы добавить в папку один или несколько конечных объектов папки, нажмите кнопку **Добавить** и укажите UNC-путь к конечному объекту папки, а затем нажмите **ОК**.


> [!TIP]
> Чтобы создать папку в пространстве имен с помощью Windows PowerShell, используйте командлет [New-DfsnFolder](/powershell/module/dfsn/new-dfsnfolder). Модуль DFSN Windows PowerShell был введен в Windows Server 2012.


## <a name="additional-references"></a>Дополнительные ссылки

-   [Развертывание пространств имен DFS](deploying-dfs-namespaces.md)
-   [Делегирование прав управления пространствами имен DFS](delegate-management-permissions-for-dfs-namespaces.md)
