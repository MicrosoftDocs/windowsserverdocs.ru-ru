---
title: Перенос параметров и данных Windows SBS 2008 на целевой сервер для миграции Windows Server Essentials
description: Узнайте, как перенести параметры и данные Windows SBS 2008 на целевой сервер для миграции Windows Server Essentials.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 4950469d-d800-430d-8d10-53bafc4a9932
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: f2e2ce873dad8a7c2e16d819ad38ed185c5b0f21
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810751"
---
# <a name="move-windows-sbs-2008-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Перенос параметров и данных Windows SBS 2008 на целевой сервер для миграции Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Перенесите параметры и данные на целевой сервер следующим образом:

1. [Копирование данных на целевой сервер](#copy-data-to-the-destination-server)

2. [Импорт Active Directory учетных записей пользователей на панель мониторинга Windows Server Essentials (необязательно)](#import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard)

3. [Перемещение роли DHCP-сервера с исходного сервера на маршрутизатор](#move-the-dhcp-server-role-from-the-source-server-to-the-router)

4. [Настройка сети](#configure-the-network)

5. [Удаление устаревших Active Directory групповая политика объектов (необязательно)](#remove-legacy-active-directory-group-policy-objects)

6. [Сопоставление разрешенных компьютеров с учетными записями пользователей](#map-permitted-computers-to-user-accounts)

## <a name="copy-data-to-the-destination-server"></a>Копирование данных на целевой сервер
Перед копированием данных с исходного сервера на целевой сервер выполните следующие действия.

- Просмотрите список общих папок на исходном сервере, включая разрешения для каждой папки. Создайте или настройте папки на целевом сервере в соответствии со структурой папок, которую вы перемещаете с исходного сервера.

- Проверьте размер каждой папки и убедитесь, что целевой сервер имеет достаточно свободного места.

- Сделайте общие папки на исходном сервере доступными только для чтения для всех пользователей, чтобы при копировании файлов на целевой сервер операции записи не выполнялись и не занимали место на диске.

#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>Копирование данных с исходного сервера на целевой сервер

1. Войдите на целевой сервер с правами администратора домена, а затем откройте окно командной строки.

2. В командной строке введите следующую команду и нажмите клавишу ВВОД:

    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`

 Где:
 - \<SourceServerName\> — имя исходного сервера
 - \<SharedSourceFolderName\> —  имя общей папки на исходном сервере
 - \<DestinationServerName\> имя целевого сервера,
 - \<SharedDestinationFolderName\> — Это общая папка на целевом сервере, куда будут копироваться данные.

3. Повторите предыдущую операцию для каждой общей папки, которую вы перемещаете с исходного сервера.

## <a name="import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard"></a>Импорт Active Directory учетных записей пользователей на панель мониторинга Windows Server Essentials
 По умолчанию все учетные записи пользователей, созданные на исходном сервере, автоматически переносятся на панель мониторинга в Windows Server Essentials. Однако процесс автоматического переноса учетной записи пользователя Active Directory завершится сбоем, если некоторые свойства не будут соответствовать требованиям миграции. Для импорта пользователей Active Directory можно использовать следующий командлет Windows PowerShell.

#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>Импорт учетной записи Active Directory пользователя на панель мониторинга Windows Server Essentials

1. Войдите на целевой сервер как администратор домена.

2. Откройте Windows PowerShell от имени администратора.

3. Запустите следующий командлет, где `[AD username]` — имя учетной записи пользователя Active Directory, которую требуется импортировать:

 `Import-WssUser SamAccountName [AD username]`

## <a name="move-the-dhcp-server-role-from-the-source-server-to-the-router"></a>Перемещение роли DHCP-сервера с исходного сервера на маршрутизатор
 Если на исходном сервер выполняется роль DHCP, для перемещения ее на маршрутизатор выполните следующие действия.

#### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>Перемещение роли DHCP с исходного сервера на маршрутизатор

1. Отключите службу DHCP на исходном сервере следующим образом:

    1. На исходном сервере нажмите кнопку **Пуск**, щелкните **Администрирование**, а затем **Службы**.

    2. В списке текущих выполняемых служб щелкните правой кнопкой мыши **DHCP-сервер**, а затем нажмите кнопку **Свойства**.

    3. Для **типа запуска** выберите **Отключено**.

    4. Остановите службу.

2. Включите роль DHCP на своем маршрутизаторе.

    1. Следуйте инструкциям в документации на маршрутизатор, чтобы включить роль DHCP на маршрутизаторе.

    2. Чтобы IP-адреса, выданные исходным сервером, остались без изменения, следуйте инструкциям в документации на маршрутизатор. Диапазон DHCP на маршрутизаторе должен быть идентичен диапазону DHCP на исходном сервере.

 > [!IMPORTANT]
 > Если статический IP-адрес или резервирования DHCP на маршрутизаторе для целевого сервера не заданы, и диапазон DHCP отличается от диапазона исходного сервера, то маршрутизатор может выдать новый IP-адрес для целевого сервера. В этом случае сбросьте правила перенаправления портов в маршрутизаторе для пересылки на новый IP-адрес целевого сервера.

## <a name="configure-the-network"></a>Настройка сети
 После переноса роли DHCP на маршрутизатор настройте параметры сети на целевом сервере.

#### <a name="to-configure-the-network"></a>Для настройки сети

1. На целевом сервере откройте панель мониторинга.

2. На панели мониторинга на **начальной** странице щелкните **Настройка**, затем **Настройка повсеместного доступа** и установите флажок **Щелкните, чтобы настроить повсеместный доступ**.

3. Выполните инструкции в мастере для настройки маршрутизатора и доменных имен.

 Если ваш маршрутизатор не поддерживает инфраструктуру UPnP, или если инфраструктура UPnP отключена, то рядом с именем маршрутизатора может появиться желтый значок предупреждения. Убедитесь, что открыты следующие порты, и что они будут направляться на IP-адрес целевого сервера.

- Порт 80: веб-трафик HTTP

- Порт 443: веб-трафик HTTPS

> [!NOTE]
> Если на втором сервере вы настроили локальный сервер Exchange Server, необходимо убедиться, что порт 25 (SMTP) также открыт и перенаправляется на IP-адрес локального сервера Exchange Server.

## <a name="remove-legacy-active-directory-group-policy-objects"></a>Удаление устаревших Active Directory объектов групповая политика
Групповая политика объекты (GPO) обновляются для Windows Server Essentials. Они являются подмножеством объектов групповой политики для Windows SBS 2008. В Windows Server Essentials для предотвращения конфликтов с объектами групповой политики Windows Server Essentials и фильтрами WMI необходимо вручную удалить ряд фильтров объектов групповой политики и инструментарий управления Windows (WMI) (WMI) Windows SBS 2008.

> [!NOTE]
> Если вы изменили исходные объекты групповой политики для Windows SBS 2008, необходимо сохранить их копии в другом месте, а затем удалить их из Windows SBS 2008.

#### <a name="to-remove-old-group-policy-objects-from-windows-sbs-2008"></a>Удаление старых объектов групповой политики из Windows SBS 2008

1. Войдите на исходный сервер как администратор.

2. Нажмите кнопку **Пуск** и выберите пункт **Управление сервером**.

3. В области навигации выберите пункт **Расширенное управление**, щелкните **Групповая политика управление**, а затем выберите **лес:** _<йоурдомаиннаме \>_.

4. Щелкните **Domains (домены**), щелкните *<йоурдомаиннаме \>*, а затем — **Групповая политика объекты**.

5. Щелкните правой кнопкой мыши **Small Business Server - политика аудита**, нажмите **Удалить**, а затем **ОК**.

6. Повторите шаг 5, чтобы удалить следующие объекты групповой политики, которые применяются к сети:

 - Клиентский компьютер Small Business Server

 - Политика паролей домена Small Business Server

Мы рекомендуем настроить политику паролей в Windows Server Essentials для принудительного применения надежных паролей. Для настройки политики паролей используйте панель мониторинга, которая записывает конфигурацию в политику домена по умолчанию. Конфигурация политики паролей не записывается в объект политики паролей домена Small Business Server, как это было в Windows SBS 2008.

 - Брандмауэр подключения к Интернету Small Business Server

 - Политика блокировки Small Business Server

 - Политика удаленного помощника Small Business Server

 - Брандмауэр Small Business Server Windows

 - Политика клиентских компьютеров служб обновления Small Business Server

 Этот объект групповой политики будет присутствовать в случае миграции с Windows SBS 2008 R2.

 - Политика общих параметров служб обновления Small Business Server

 Этот объект групповой политики будет присутствовать в случае миграции с Windows SBS 2008 R2.

 - Политика серверных компьютеров служб обновления Small Business Server

 Этот объект групповой политики будет присутствовать в случае миграции с Windows SBS 2008 R2.

7. Убедитесь, что все объекты групповой политики удалены.

#### <a name="to-remove-wmi-filters-from-windows-sbs-2008"></a>Удаление фильтров WMI из Windows SBS 2008

1. Войдите на исходный сервер как администратор.

2. Нажмите кнопку **Пуск** и выберите пункт **Управление сервером**.

3. В области навигации выберите пункт **Расширенное управление**, щелкните **Групповая политика управление**, а затем выберите **лес:** _<йоурнетворкдомаиннаме \>_ .

4. Щелкните **домены**, щелкните *<\> йоурнетворкдомаиннаме*, а затем щелкните **фильтры WMI**.

5. Щелкните правой кнопкой мыши **PostSP2**, нажмите **Удалить**, а затем **Да**.

6. Щелкните правой кнопкой мыши **PreSP2**, нажмите **Удалить**, а затем **Да**.

7. Убедитесь, что эти фильтры WMI удалены.

## <a name="map-permitted-computers-to-user-accounts"></a>Сопоставление разрешенных компьютеров с учетными записями пользователей
Если пользователь подключается к удаленному веб-доступу в Windows SBS 2008, то отображаются все компьютеры в сети. Среди них также могут быть компьютеры, разрешения на доступ к которым у пользователя нет. В Windows Server Essentials пользователь должен быть явно назначен компьютеру для отображения в удаленном Веб-доступ. Каждая учетная запись пользователя, которая переносится с Windows SBS 2008, должна быть сопоставлена с одним или несколькими компьютерами.

#### <a name="to-map-user-accounts-to-computers"></a>Сопоставление учетных записей и компьютеров

1. Откройте панель мониторинга Windows Server Essentials.

2. На панели навигации щелкните **Пользователи**.

3. В списке учетных записей пользователей щелкните правой кнопкой мыши учетную запись пользователя и нажмите кнопку **Просмотреть свойства учетной записи**.

4. Перейдите на вкладку **Повсеместный доступ**, а затем установите флажок **Разрешить удаленный веб-доступ и доступ к веб-приложениям служб**.

5. Выберите **Общие папки**, затем **Компьютеры**, затем **Ссылки главной страницы** и нажмите кнопку **Применить**.

6. Перейдите на вкладку **Доступ к компьютеру**, а затем щелкните имя компьютера, доступ к которому вы хотите разрешить.

7. Повторите шаги 3, 4, 5 и 6 для каждой учетной записи пользователя.

> [!NOTE]
> Конфигурацию клиентского компьютера изменять не нужно. Она настраивается автоматически.
>
> По окончании процесса миграции, если при создании первой новой учетной записи пользователя на целевом сервере появится проблема, удалите добавленную учетную запись пользователя, а затем создайте ее снова.
