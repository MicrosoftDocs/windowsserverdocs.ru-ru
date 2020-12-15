---
description: 'Сведения по таким темам: Перенос репликации SYSVOL в репликацию DFS'
title: Перенос репликации SYSVOL в репликацию DFS
ms.date: 07/02/2012
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: c0ab678542260b9b7d1975a633b2244aac7fe3d7
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97048762"
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

[Серия о миграции SYSVOL. Часть 1. Общие сведения о процессе миграции SYSVOL](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-1-8211-introduction-to-the-sysvol/ba-p/423456)

[Серия о миграции SYSVOL. Часть 2. Dfsrmig.exe: средство миграции SYSVOL](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-2-8211-dfsrmig-exe-the-sysvol/ba-p/423470)

[Серия о миграции SYSVOL. Часть 3. Переход в состояние PREPARED](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-3-migrating-to-the-prepared-state/ba-p/423503)

[Серия о миграции SYSVOL. Часть 4 Переход в состояние REDIRECTED](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-4-8211-migrating-to-the-8216/ba-p/423514)

[Серия о миграции SYSVOL. Часть 5 Переход в состояние ELIMINATED](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-5-8211-migrating-to-the-8216/ba-p/423516)

[Пошаговое руководство. Использование распределенной файловой системы в Windows Server 2008](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732863(v=ws.10))

[Технический справочник по FRS](/previous-versions/windows/it-pro/windows-server-2003/cc759297(v=ws.10))
