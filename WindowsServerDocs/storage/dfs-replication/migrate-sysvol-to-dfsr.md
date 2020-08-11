---
title: Перенос репликации SYSVOL в репликацию DFS
ms.date: 07/02/2012
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 6e022e4fdae631199bacca5f67c7953125ddd141
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950738"
---
# <a name="migrate-sysvol-replication-to-dfs-replication"></a>Перенос репликации SYSVOL в репликацию DFS


Обновлено: 25 августа 2010 г.

Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

Контроллеры домена используют специальную общую папку с именем SYSVOL для репликации скриптов входа в систему и файлов объекта групповой политики на другие контроллеры домена. Windows 2000 Server и Windows Server 2003 используют для репликации SYSVOL службу репликации файлов (FRS), тогда как Windows Server 2008 использует более новую службу "Репликация DFS" в доменах с режимом работы Windows Server 2008, или FRS для доменов с более старыми режимами работы.

Чтобы использовать репликацию DFS для репликации папки SYSVOL, вы можете создать новый домен с режимом работы Windows Server 2008 либо выполнить описанную в этом документе процедуру, которая обновит существующий домен и перенесет репликацию в службу "Репликация DFS".

В этом документе предполагается, что у вас есть базовые знания о доменных службах Active Directory (AD DS), FRS и репликации DFS (репликация распределенной файловой системы). Дополнительные сведения см. в статьях [Обзор доменных служб Active Directory](https://go.microsoft.com/fwlink/?linkid=147787), [Обзор FRS](https://go.microsoft.com/fwlink/?linkid=121763) и (или) [Обзор репликации DFS](https://go.microsoft.com/fwlink/?linkid=121762).


> [!NOTE]
> Вы можете скачать подготовленную для печати версию <a href="https://go.microsoft.com/fwlink/?linkid=150375">руководства по миграции репликации SYSVOL из FRS в Репликацию DFS</a> (https://go.microsoft.com/fwlink/?LinkId=150375)
<br>


## <a name="in-this-guide"></a>В данном руководстве

[Концептуальные сведения о миграции SYSVOL](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640170(v=ws.10))

  - [Состояния миграции SYSVOL](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641052(v=ws.10))

  - [Общие сведения о процедуре миграции SYSVOL](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639809(v=ws.10))


[Процедура миграции SYSVOL](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639860(v=ws.10))

  - [Переход в подготовленное состояние](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641193(v=ws.10))

  - [Переход в перенаправленное состояние](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641340(v=ws.10))

  - [Переход в исключенное состояние](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640254(v=ws.10))


[Устранение неполадок при миграции SYSVOL](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640395(v=ws.10))

  - [Устранение проблем с миграцией SYSVOL](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639976(v=ws.10))

  - [Откат миграции SYSVOL в предыдущее стабильное состояние](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640509(v=ws.10))


[Справочная информация о миграции SYSVOL](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640293(v=ws.10))

  - [Поддерживаемые сценарии миграции SYSVOL](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639854(v=ws.10))

  - [Проверка состояния миграции SYSVOL](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639789(v=ws.10))

  - [Dfsrmig](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641227(v=ws.10))

  - [Действия в средстве миграции SYSVOL](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639712(v=ws.10))


## <a name="additional-references"></a>Дополнительная справка

[Серия о миграции SYSVOL. Часть 1 — общие сведения о процедуре миграции SYSVOL](https://go.microsoft.com/fwlink/?linkid=121756)

[Серия о миграции SYSVOL. Часть 2 — Dfsrmig.exe: средство миграции SYSVOL](https://go.microsoft.com/fwlink/?linkid=121757)

[Серия о миграции SYSVOL. Часть 3 — переход в состояние PREPARED](https://go.microsoft.com/fwlink/?linkid=121758)

[Серия о миграции SYSVOL. Часть 4 — переход в состояние REDIRECTED](https://go.microsoft.com/fwlink/?linkid=121759)

[Серия о миграции SYSVOL. Часть 5 — переход в состояние ELIMINATED](https://go.microsoft.com/fwlink/?linkid=121760)

[Пошаговое руководство по распределенной файловой системе в Windows Server 2008](https://go.microsoft.com/fwlink/?linkid=85231)

[Технический справочник по FRS](https://go.microsoft.com/fwlink/?linkid=121764)
