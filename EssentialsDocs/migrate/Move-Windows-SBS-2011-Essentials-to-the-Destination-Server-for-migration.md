---
title: Перенос параметров и данных Windows SBS 2011 Essentials на целевой сервер для миграции Windows Server Essentials
description: Узнайте, как перенести параметры и данные Windows SBS 2011 Essentials на целевой сервер для миграции Windows Server Essentials.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 47548994-9fa0-42e0-afa4-c2ccbd063acb
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 25a155db15f0ea76695c1bbbda100d18e1c56b9a
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810712"
---
# <a name="move-windows-sbs-2011-essentials-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Перенос параметров и данных Windows SBS 2011 Essentials на целевой сервер для миграции Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Перенесите параметры и данные на целевой сервер следующим образом:


1.  [Копирование данных на целевой сервер](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_CopyData)

2.  [Импорт Active Directory учетных записей пользователей на панель мониторинга Windows Server Essentials (необязательно)](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_ImportADaccounts)

3.  [Настройка сети](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_Network)

4.  [Сопоставление разрешенных компьютеров с учетными записями пользователей](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_MapPermittedComputers)

##  <a name="copy-data-to-the-destination-server"></a><a name="BKMK_CopyData"></a> Копирование данных на целевой сервер
 Перед копированием данных с исходного сервера на целевой сервер выполните следующие действия.

-   Просмотрите список общих папок на исходном сервере, включая разрешения для каждой папки. Создайте или настройте папки на целевом сервере в соответствии со структурой папок, которую вы перемещаете с исходного сервера.

-   Проверьте размер каждой папки и убедитесь, что целевой сервер имеет достаточно свободного места.

-   Сделайте общие папки на исходном сервере доступными только для чтения для всех пользователей, чтобы при копировании файлов на целевой сервер операции записи не выполнялись и не занимали место на диске.

#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>Копирование данных с исходного сервера на целевой сервер

1.  Войдите на целевой сервер с правами администратора домена, а затем откройте окно командной строки.

2.  В командной строке введите следующую команду и нажмите клавишу ВВОД:

    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`

     Где:
     - \<SourceServerName\> — имя исходного сервера
     - \<SharedSourceFolderName\> —  имя общей папки на исходном сервере
     - \<DestinationServerName\> имя целевого сервера,
     - \<SharedDestinationFolderName\> — Это общая папка на целевом сервере, куда будут копироваться данные.

3.  Повторите предыдущую операцию для каждой общей папки, которую вы перемещаете с исходного сервера.

##  <a name="import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard-optional"></a><a name="BKMK_ImportADaccounts"></a> Импорт Active Directory учетных записей пользователей на панель мониторинга Windows Server Essentials (необязательно)
 По умолчанию все учетные записи пользователей, созданные на исходном сервере, автоматически переносятся на панель мониторинга в Windows Server Essentials. Однако процесс автоматического переноса учетной записи пользователя Active Directory завершится сбоем, если все свойства не будут соответствовать требованиям миграции. Для импорта пользователей Active Directory можно использовать следующий командлет Windows PowerShell.

#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>Импорт учетной записи Active Directory пользователя на панель мониторинга Windows Server Essentials

1.  Войдите на целевой сервер как администратор домена.

2.  Откройте Windows PowerShell от имени администратора.

3.  Запустите следующий командлет, где `[AD username]` — имя учетной записи пользователя Active Directory, которую требуется импортировать:

     `Import-WssUser  SamAccountName [AD username]`

##  <a name="configure-the-network"></a><a name="BKMK_Network"></a> Настройка сети

#### <a name="to-configure-the-network"></a>Для настройки сети

1. На целевом сервере откройте панель мониторинга.

2. На панели мониторинга на **начальной** странице щелкните **Настройка**, затем **Настройка повсеместного доступа** и установите флажок **Щелкните, чтобы настроить повсеместный доступ**.

3. Выполните инструкции в мастере для настройки маршрутизатора и доменных имен.

   Если ваш маршрутизатор не поддерживает инфраструктуру UPnP, или если инфраструктура UPnP отключена, то рядом с именем маршрутизатора может появиться желтый значок предупреждения. Убедитесь, что открыты следующие порты, и что они будут направляться на IP-адрес целевого сервера.

-   Порт 80: веб-трафик HTTP

-   Порт 443: веб-трафик HTTPS

##  <a name="map-permitted-computers-to-user-accounts"></a><a name="BKMK_MapPermittedComputers"></a> Сопоставьте разрешенные компьютеры учетным записям пользователей
 Каждая учетная запись пользователя, которая переносится из Windows Small Business Server 2011 Essentials, должна быть сопоставлена с одним или несколькими компьютерами.

#### <a name="to-map-user-accounts-to-computers"></a>Сопоставление учетных записей и компьютеров

1.  Откройте панель мониторинга Windows Server Essentials.

2.  На панели навигации щелкните **Пользователи**.

3.  В списке учетных записей пользователей щелкните правой кнопкой мыши учетную запись пользователя и нажмите кнопку **Просмотреть свойства учетной записи**.

4.  Перейдите на вкладку **Повсеместный доступ**, а затем установите флажок **Разрешить удаленный веб-доступ и доступ к веб-приложениям служб**.

5.  Выберите **Общие папки**, затем **Компьютеры**, затем **Ссылки главной страницы** и нажмите кнопку **Применить**.

6.  Перейдите на вкладку **Доступ к компьютеру**, а затем щелкните имя компьютера, доступ к которому вы хотите разрешить.

7.  Повторите шаги 3, 4, 5 и 6 для каждой учетной записи пользователя.

> [!NOTE]
>  Конфигурацию клиентского компьютера изменять не нужно. Она настраивается автоматически.

> [!NOTE]
>  По окончании процесса миграции, если при создании первой новой учетной записи пользователя на целевом сервере появится проблема, удалите добавленную учетную запись пользователя, а затем создайте ее снова.
