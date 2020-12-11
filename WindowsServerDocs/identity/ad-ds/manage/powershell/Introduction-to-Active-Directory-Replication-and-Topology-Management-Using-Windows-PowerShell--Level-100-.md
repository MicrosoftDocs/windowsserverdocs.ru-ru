---
description: Дополнительные сведения см. в статьях общие сведения о репликации Active Directory и управлении топологией с помощью Windows PowerShell (уровень 100).
ms.assetid: c54b544f-cc32-4837-bb2d-a8656b22f3de
title: Introduction to Active Directory Replication and Topology Management Using Windows PowerShell (Level 100)
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 74072794f45a7eb6b56be294ef288a4d518398b0
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97046382"
---
# <a name="introduction-to-active-directory-replication-and-topology-management-using-windows-powershell-level-100"></a>Introduction to Active Directory Replication and Topology Management Using Windows PowerShell (Level 100)

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows PowerShell для Active Directory предоставляет возможность управления репликацией, сайтами, доменами и лесами, контроллерами доменов и разделами. Пользователи предыдущих средств управления, таких как оснастка "Active Directory – сайты и службы" и repadmin.exe, обратят внимание на то, что похожая функциональность теперь доступна в рамках Windows PowerShell для контекста Active Directory. Кроме того, командлеты совместимы с существующими командлетами Windows PowerShell для Active Directory, что приводит к созданию упрощенного взаимодействия и позволяет пользователям легко создавать сценарии автоматизации.

> [!NOTE]
> Командлеты Windows PowerShell для репликации и топологии Active Directory доступны в следующих средах:
>
> -    Контроллер домена Windows Server 2012
> -    Windows Server 2012 с средства удаленного администрирования сервера для AD DS и AD LDS.
> -   Windows &reg; 8 с средства удаленного администрирования сервера для AD DS и AD LDS.

## <a name="installing-the-active-directory-module-for-windows-powershell"></a>Установка модуля Active Directory для Windows PowerShell
Модуль Active Directory для Windows PowerShell устанавливается по умолчанию, когда роль сервера AD DS установлена на сервере под управлением Windows Server 2012. Дополнительные действия, помимо добавления роли сервера, не требуются. Кроме того, модуль Active Directory можно установить на сервере под управлением Windows Server 2012, установив средства удаленного администрирования сервера, и можно установить модуль Active Directory на компьютере с Windows 8, загрузив и установив [средства удаленного администрирования сервера (RSAT)](https://www.microsoft.com/download/details.aspx?id=28972). Установка описывается в разделе [Инструкции](https://www.microsoft.com/download/details.aspx?id=28972).

## <a name="scenarios-for-testing-windows-powershell-for-active-directory-replication-and-topology-management-cmdlets"></a>Сценарии для тестирования командлетов управления репликацией и топологией Windows PowerShell для Active Directory
Следующие сценарии предназначены для ознакомления администраторов с новыми командлетами управления:

-   Получение списка всех контроллеров доменов и соответствующих сайтов

-   Управление топологией репликации

-   Просмотр состояния и сведений о репликации

## <a name="lab-requirements"></a>Лабораторные требования

-   Два контроллера домена Windows Server 2012: **DC1** и **DC2** , которые являются частью домена contoso.com и находятся на корпоративном сайте в пределах этого домена.

## <a name="view-domain-controllers-and-their-sites"></a>Просмотр контроллеров домена и соответствующих сайтов
На этом этапе с помощью модуля Active Directory для Windows PowerShell можно просмотреть существующие контроллеры домена и топологию репликации для домена.

Для завершения шагов в следующих процедурах вам необходимо быть членом группы "Администраторы домена" или иметь аналогичные разрешения.

#### <a name="to-view-all-active-directory-sites"></a>Просмотр всех узлов Active Directory

1.  На контроллере **DC1** щелкните **Windows PowerShell** на панели задач.

2.  Введите следующую команду:

    `Get-ADReplicationSite -Filter *`

    При этом возвращаются подробные сведения о каждом сайте. Параметр `Filter` используется во всех командлетах AD PowerShell для ограничения списка возвращаемых объектов. В этом случае звездочка (*) означает все объекты сайта.

    > [!TIP]
    > Для автозаполнения команд в Windows PowerShell можно использовать клавишу TAB.
    >
    > Пример. Введите `Get-ADRep` и нажмите клавишу TAB несколько раз, чтобы пропустить совпадающие команды, пока не достигнете команды `Get-ADReplicationSite`. Автозаполнение также работает для имен параметров, таких как `Filter`.

    Чтобы отформатировать выходные данные `Get-ADReplicationSite` команды в виде таблицы и ограничить отображение конкретными полями, можно передать результат в `Format-Table` команду (или " `ft` " для краткости):

    `Get-ADReplicationSite -Filter * | ft Name`

    При этом возвращается краткая версия списка сайтов, включающая только поле "Имя".

#### <a name="to-produce-a-table-of-all-domain-controllers"></a>Создание таблицы всех контроллеров домена

-   Введите следующую команду в командной строке **модуля Active Directory для Windows PowerShell**:

    `Get-ADDomainController -Filter * | ft Hostname,Site`

    Эта команда возвращает имя узла контроллеров домена, а также их связи с сайтами.

## <a name="manage-replication-topology"></a>Управление топологией репликации
На предыдущем шаге после выполнения команды `Get-ADDomainController -Filter * | ft Hostname,Site` контроллер домена **DC2** входил в список сайта **CORPORATE**. В процедурах ниже описано создание нового сайта филиала **BRANCH1**, создание новой связи сайтов, задание стоимости связи сайтов и частоты репликации и перемещение **DC2** в **BRANCH1**.

Для завершения шагов в следующих процедурах вам необходимо быть членом группы "Администраторы домена" или иметь аналогичные разрешения.

#### <a name="to-create-a-new-site"></a>Создание нового сайта

-   Введите следующую команду в командной строке **модуля Active Directory для Windows PowerShell**:

    `New-ADReplicationSite BRANCH1`

    С помощью этой команды создается новый сайт филиала branch1.

#### <a name="to-create-a-new-site-link"></a>Создание новой связи сайтов

-   Введите следующую команду в командной строке **модуля Active Directory для Windows PowerShell**:

    `New-ADReplicationSiteLink 'CORPORATE-BRANCH1'  -SitesIncluded CORPORATE,BRANCH1 -OtherAttributes @{'options'=1}`

    С помощью этой команды создается связь сайтов с **BRANCH1** и включается процесс уведомления об изменении.

    > [!TIP]
    > Чтобы не вводить вручную имена параметров, например `-SitesIncluded` и `-OtherAttributes`, можно использовать автозаполнение с помощью клавиши табуляции.

#### <a name="to-set-the-site-link-cost-and-replication-frequency"></a>Задание стоимости связи сайтов и частоты репликации

-   Введите следующую команду в командной строке **модуля Active Directory для Windows PowerShell**:

    `Set-ADReplicationSiteLink CORPORATE-BRANCH1 -Cost 100 -ReplicationFrequencyInMinutes 15`

    С помощью этой команды задается стоимость связи сайтов с **BRANCH1**, равная **100**, и частота репликации с сайтом **15 минут**.

#### <a name="to-move-a-domain-controller-to-a-different-site"></a>Перемещение контроллера домена на другой сайт

-   Введите следующую команду в командной строке **модуля Active Directory для Windows PowerShell**:

    `Get-ADDomainController DC2 | Move-ADDirectoryServer -Site BRANCH1`

    С помощью этой команды контроллер домена **DC2** перемещается на сайт **BRANCH1**.

### <a name="verification"></a>Проверка

##### <a name="to-verify-site-creation-new-site-link-and-cost-and-replication-frequency"></a>Проверка создания сайта, новой связи сайтов и стоимости и частоты репликации

-   Щелкните **Server Manager**, выберите пункт **Средства**, затем **Active Directory – сайты и службы** и проверьте следующее.

    Убедитесь, что сайт **BRANCH1** содержит все правильные значения из команд Windows PowerShell.

    Убедитесь, что создана связь сайтов **CORPORATE-BRANCH1**, соединяющая сайты **BRANCH1** и **CORPORATE**.

    Убедитесь, что **DC2** сейчас находится на сайте **BRANCH1**. Можно также открыть **Модуль Active Directory для Windows PowerShell** и, чтобы убедиться, что **DC2** сейчас находится на сайте **BRANCH1**, ввести следующую команду: `Get-ADDomainController -Filter * | ft Hostname,Site`.

## <a name="view-replication-status-information"></a>Просмотр состояния и сведений о репликации.
В следующих процедурах с помощью одного из командлетов управления репликацией Windows PowerShell для Active Directory, `Get-ADReplicationUpToDatenessVectorTable DC1` можно создать простой отчет о репликации с использованием векторной таблицы синхронизации, которая ведется на контроллере домена. В этой векторной таблице синхронизации отслеживается наивысший номер последовательного обновления (USN) создаваемой записи, отображаемый на каждом контроллере домена в лесу.

Для завершения шагов в следующих процедурах вам необходимо быть членом группы "Администраторы домена" или иметь аналогичные разрешения.

#### <a name="to-view-the-up-to-dateness-vector-table-for-a-single-domain-controller"></a>Просмотр векторной таблицы синхронизации для одного контроллера домена

1.  Введите следующую команду в командной строке **модуля Active Directory для Windows PowerShell**:

    `Get-ADReplicationUpToDatenessVectorTable DC1`

    При этом выводится список наивысших номеров последовательного обновления (USN), отображаемый на **DC1** для каждого контроллера домена в лесу. Значение параметра **Сервер** относится к серверу, на котором ведется таблица: в данном случае — **DC1**. Значение параметра **Партнер** относится к партнеру репликации (прямому или непрямому), в связи с которым были внесены изменения. Значение параметра UsnFilter является наивысшим номером последовательного обновления (USN), отображаемым на **DC1** для партнера. Если новый контроллер домена добавлен в лес, он не появится в таблице **DC1** до тех пор, пока **DC1** не получит изменения, поступающие из нового домена.

#### <a name="to-view-the-up-to-dateness-vector-table-for-all-domain-controllers-in-a-domain"></a>Просмотр векторной таблицы синхронизации для всех контроллеров домена в домене

1.  Введите следующую команду в командной строке "Модуль Active Directory для Windows PowerShell":

    `Get-ADReplicationUpToDatenessVectorTable * | sort Partner,Server | ft Partner,Server,UsnFilter`

    С помощью этой команды **DC1** меняется на `*`, что приводит к сбору данных векторной таблицы синхронизации со всех контроллеров домена. Данные сортируются по параметрам **Партнер** и **Сервер**, а затем отображаются в таблице.

    Сортировка позволяет легко сравнить последний номер последовательного обновления (USN), отображаемый на каждом контроллере домена для данного партнера репликации. Это быстрый способ убедиться, что репликация проходит во всей среде. Если репликация работает правильно, то значения параметра UsnFilter, указанные в отчете для данного партнера репликации, должны быть похожи на всех контроллерах домена.

## <a name="see-also"></a>См. также:
[Расширенная репликация Active Directory и управление топологией с помощью Windows PowerShell &#40;уровня 200&#41;](Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md)


