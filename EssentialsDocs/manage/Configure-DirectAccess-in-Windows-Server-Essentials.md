---
title: Настройка DirectAccess в Windows Server Essentials
description: Узнайте, как настроить DirectAccess, чтобы позволить мобильным сотрудникам подключаться к сети из любого удаленного расположения, не устанавливая VPN-подключение.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: c959b6fc-c67e-46cd-a9cb-cee71a42fa4c
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: eb24f45e301bb616c7d8a43dbf4151c0b8af1ac7
ms.sourcegitcommit: e00e789dff216dbade861e61365f078b758a5720
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2020
ms.locfileid: "97755340"
---
# <a name="configure-directaccess-in-windows-server-essentials"></a>Настройка DirectAccess в Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

В этом разделе приводятся пошаговые инструкции по настройке DirectAccess в Windows Server Essentials, позволяющие мобильным сотрудникам легко подключаться к сети организации из любого удаленного расположения в Интернете, не устанавливая подключение к виртуальной частной сети (VPN). DirectAccess может предлагать мобильным работникам те же возможности подключения внутри и за пределами офиса Windows 8.1, Windows 8 и Windows 7.

 В Windows Server Essentials, если домен содержит более одного сервера Windows Server Essentials, на контроллере домена необходимо настроить DirectAccess.

> [!NOTE]
>  В этом разделе приводятся инструкции по настройке DirectAccess, когда сервер Windows Server Essentials является контроллером домена. Если сервер Windows Server Essentials является членом домена, следуйте инструкциям по настройке DirectAccess на члене домена в разделе [Добавление DirectAccess в существующее развертывание с помощью удаленного доступа (VPN)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574220(v=ws.11)) .

## <a name="process-overview"></a>Общие сведения о процессе
 Чтобы настроить DirectAccess в Windows Server Essentials, выполните следующие действия.

> [!IMPORTANT]
>  Прежде чем использовать процедуры из этого руководств для настройки DirectAccess в Windows Server Essentials, необходимо включить VPN на сервере. Инструкции см. в разделе [Управление VPN](Manage-VPN-in-Windows-Server-Essentials.md).

-   [Шаг 1. Добавление на сервер средства управления удаленным доступом](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddRAM)

-   [Шаг 2. Изменение адреса сетевого адаптера сервера на статический IP-адрес](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddStaticIP)

-   [Шаг 3. Подготовка сертификата и запись DNS для сервера сетевых расположений](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)

    -   [Шаг 3a. предоставление полного доступа пользователям, прошедшим проверку подлинности, для шаблона сертификата веб-сервера](#BKMK_GrantFullPermissions)

    -   [Шаг 3б. Регистрация сертификата для сервера сетевых расположений с общим именем, которое невозможно разрешить из внешней сети](#BKMK_EnrollaCertificate)

    -   [Шаг 3c. Добавьте новый узел на DNS-сервере и сопоставьте его с адресом сервера Windows Server Essentials.](#BKMK_MapNewHosttoServerAddress)

-   [Шаг 4. Создание группы безопасности для клиентских компьютеров DirectAccess](#BKMK_AddSecurityGroup)

-   [Шаг 5. Включение и настройка DirectAccess](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableConfigureDA)

    -   [Шаг 5а. Включение DirectAccess через консоль управления удаленным доступом](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)

    -   [Шаг 5b. Удаление недопустимого IPv6Prefix в объекте групповой политики RRAS (только для Windows Server Essentials)](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)

    -   [Шаг 5в. Настройка DirectAccess на клиентских компьютерах под управлением Windows 7 Enterprise](#BKMK_Step4cWindows7Setup)

    -   [Шаг 5г. Настройка сервера сетевых расположений](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)

    -   [Шаг 5д. Добавление раздела реестра для обхода сертификации ЦС при установке канала IPsec](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)

-   [Шаг 6. Настройка параметров таблицы политики разрешения имен для сервера DirectAccess](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NRPT)

-   [Шаг 7. Настроить правила брандмауэра TCP и UDP для объектов групповой политики сервера DirectAccess.](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_TCPUDP)

-   [Шаг 8. Изменить конфигурацию DNS64 для ожидания передачи данных интерфейса IP-HTTPS.](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS64)

-   [Шаг 9. Резервирование портов для службы WinNat](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_ExemptPort)

-   [Шаг 10. Перезапуск службы WinNat](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_WinNAT)

> [!NOTE]
>  [Приложение: Установка DirectAccess с помощью Windows PowerShell](#BKMK_AppendixBPowerShellScript) предусматривает настройку DirectAccess с помощью сценария Windows PowerShell.

##  <a name="step-1-add-remote-access-management-tools-to-your-server"></a><a name="BKMK_AddRAM"></a> Шаг 1. Добавление средств управления удаленным доступом на сервер

#### <a name="to-add-remote-accregss-management-tools--reg"></a>Добавление удаленных &reg; средств управления ACC SS  &reg;

1.  На сервере щелкните значок **Диспетчер серверов** в левом нижнем углу начальной страницы.

     В Windows Server Essentials необходимо будет выполнить поиск диспетчер сервера, чтобы открыть его. На начальной странице введите **Server Manager**, после чего щелкните **Диспетчер серверов** в результатах поиска. Чтобы поместить диспетчер серверов на начальный экран, щелкните его правой кнопкой мыши в результатах поиска и нажмите **Закрепить на начальном экране**.

2.  Если отобразится предупреждающее сообщение **Контроля учетных записей**, щелкните **Да**.

3.  На панели мониторинга диспетчера серверов щелкните **Управление**, после чего нажмите **Добавить роли и компоненты**.

4.  В мастере добавления ролей и компонентов выполите следующие действия:

    1.  На странице **Тип установки** щелкните **Установка ролей или компонентов**.

    2.  На **странице Выбор сервера** (или на странице **Выбор целевого сервера** в Windows Server Essentials) щелкните **выбрать сервер в пуле серверов**.

    3.  На странице **Возможности** разверните **Средства удаленного администрирования сервера (установлены)**, затем **Средства управления удаленным доступом (установлены)**, щелкните **Средства администрирования ролей (установлены)**, откройте **Средства управления удаленным доступом**, после чего выберите **Графический интерфейс пользователя удаленного доступа и программы командной строки**.

    4.  Для завершения работы мастера следуйте инструкциям на экране.

##  <a name="step-2-change-the-network-adapter-address-of-the-server-to-a-static-ip-address"></a><a name="BKMK_AddStaticIP"></a> Шаг 2. изменение адреса сетевого адаптера сервера на статический IP-адрес
 Для работы компонента DirectAccess необходим адаптер со статическим IP-адресом. Следует изменить IP-адрес локального сетевого адаптера на сервере.

#### <a name="to-add-a-static-ip-address"></a>Добавление статического IP-адреса

1.  На начальной странице откройте **Панель управления**.

2.  Щелкните **Сеть и Интернет**, а затем **Просмотр состояния сети и задач**.

3.  В области задач **Центра управления сетями и общим доступом** щелкните **Изменение параметров адаптера**.

4.  Щелкните правой кнопкой мыши локальный сетевой адаптер, а затем щелкните **Свойства**.

5.  На вкладке **Сеть** выберите **Протокол Интернета версии 4 (TCP/IPv4)** и нажмите кнопку **Свойства**.

6.  На вкладке **Общие** щелкните **Использовать следующий IP-адрес** и введите нужный IP-адрес.

     В поле **Маска подсети** автоматически появится значение по умолчанию для маски подсети. Примите значение по умолчанию или введите нужное значение маски подсети.

7.  В поле **Шлюз по умолчанию** введите IP-адрес шлюза по умолчанию.

8.  В поле **Предпочитаемый DNS-сервер** введите IP-адрес DNS-сервера.

    > [!NOTE]
    >  Вместо IP замыкаемой на себя сети (например,127.0.0.1) следует использовать IP-адрес, который был назначен вашему сетевому адаптеру DHCP (например, 192.168.X.X). Чтобы узнать назначенный IP-адрес, введите в командной строке **ipconfig**.

9. В поле **Альтернативный DNS-сервер** введите IP-адрес альтернативного DNS-сервера (если есть).

10. Нажмите кнопку **ОК**, затем кнопку **Закрыть**.

> [!IMPORTANT]
>  Убедитесь, что маршрутизатор настроен на перенаправление портов 80 и 443 новому статическому IP-адресу сервера.

##  <a name="step-3-prepare-a-certificate-and-dns-record-for-the-network-location-server"></a><a name="BKMK_DNS"></a> Шаг 3. Подготовка сертификата и записи DNS для сервера сетевого расположения
 Чтобы подготовить сертификат и произвести запись DNS для сервера сетевых расположений, выполните следующие действия:

-   [Шаг 3a. предоставление полного доступа пользователям, прошедшим проверку подлинности, для шаблона сертификата веб-сервера](#BKMK_GrantFullPermissions)

-   [Шаг 3б. Регистрация сертификата для сервера сетевых расположений с общим именем, которое невозможно разрешить из внешней сети](#BKMK_EnrollaCertificate)

-   [Шаг 3в. Добавление нового узла к DNS-серверу и сопоставление его с адресом сервера под управлением Windows Server Essentials.](#BKMK_MapNewHosttoServerAddress)

###  <a name="step-3a-grant-full-permissions-to-authenticated-users-for-the-web-servers-certificate-template"></a><a name="BKMK_GrantFullPermissions"></a> Шаг 3a. предоставление полного доступа пользователям, прошедшим проверку подлинности, для шаблона сертификата веб-сервера
 Первая задача — предоставить полный доступ для проверки подлинности пользователей для шаблона сертификата веб-сервера в центре сертификации.

####  <a name="to-grant-full-permissions-to-authenticated-users-for-the-web-servers-certificate-template"></a><a name="BKMK_ToGrantFullPermissions"></a> Предоставление полного доступа пользователям, прошедшим проверку подлинности, для шаблона сертификата веб-сервера

1.  На **Начальной странице** откройте **Центр сертификации**.

2.  В дереве консоли в разделе **центр сертификации (локальный)** разверните **<ServerName \> -CA**, щелкните правой кнопкой мыши **шаблоны сертификатов**, а затем выберите пункт **Управление**.

3.  В разделе **Центр сертификации (Локальный)** щелкните правой кнопкой мыши **Веб-сервер**, после чего нажмите **Свойства**.

4.  В свойствах веб-сервера на вкладке **Безопасность** щелкните **Прошедшие проверку**, выберите **Полный доступ**, а затем нажмите **OК**.

5.  Перезапустите **Службы сертификатов Active Directory**. В панели управления выберите **Просмотр локальных служб**. В списке служб щелкните правой кнопкой мыши **Службы сертификатов Active Directory**, после чего нажмите **Перезапуск**.

###  <a name="step-3b-enroll-a-certificate-for-the-network-location-server-with-a-common-name-that-is-unresolvable-from-the-external-network"></a><a name="BKMK_EnrollaCertificate"></a> Шаг 3b. регистрация сертификата для сервера сетевых расположений с общим именем, неразрешимым из внешней сети
 После этого необходимо выполнить регистрацию сертификата для сервера сетевых расположений с общим именем, которое невозможно разрешить из внешней сети.

####  <a name="to-enroll-a-certificate-for-the-network-location-server"></a><a name="BKMK_ToEnrollaCertificate"></a> Регистрация сертификата для сервера сетевых расположений

1.  На **Начальной странице** откройте **mmc** (консоль управления).

2.  Если появится предупреждающее сообщение **Контроля учетных записей**, щелкните **Да**.

     Отобразится консоль управления (MMC).

3.  В меню **Файл** щелкните **Добавить или удалить оснастку**.

4.  В поле **Добавить или удалить оснастку** щелкните **Сертификаты**, после чего нажмите **Добавить**.

5.  На странице **Оснастка диспетчера сертификатов** щелкните **Учетная запись компьютера** и нажмите кнопку **Далее**.

6.  На странице **Выбор компьютера** щелкните **Локальный компьютер**, нажмите кнопку **Готово**, а затем **ОК**.

7.  В дереве консоли разверните **Сертификаты (локальный компьютер)**, затем **Личные**, щелкните правой кнопкой мыши **Сертификаты**, после чего в области **Все задачи** нажмите **Запросить новый сертификат**.

8.  Когда откроется мастер регистрации сертификатов, щелкните **Далее**.

9. На странице **Выбор политики регистрации сертификатов** щелкните **Далее**.

10. На странице **Запросить сертификат** поставьте флажок рядом с пунктом **Веб-сервер**, после чего щелкните **Для регистрации этого сертификата необходимы дополнительные сведения**.

11. В поле **Свойства сертификата** установите следующие параметры для пункта **Имя субъекта**:

    1.  Для параметра **Тип** выберите **Общее имя**.

    2.  Для параметра **Значение** введите имя сервера сетевых расположений (например, DirectAccess-NLS.contoso.local), а затем щелкните **Добавить**.

    3.  Нажмите кнопку **ОК**, после чего щелкните **Регистрация**.

12. По завершении регистрации сертификата щелкните кнопку **Готово**.

###  <a name="step-3c-add-a-new-host-on-the-dns-server-and-map-it-to-the-windows-server-essentials-server-address"></a><a name="BKMK_MapNewHosttoServerAddress"></a> Шаг 3c. Добавьте новый узел на DNS-сервере и сопоставьте его с адресом сервера Windows Server Essentials.
 Чтобы завершить настройку DNS, добавьте новый узел на DNS-сервере и сопоставьте его с адресом сервера Windows Server Essentials.

####  <a name="to-map-a-new-host-to-the-windows-server-essentials-server-address"></a><a name="BKMK_ToMapNewHosttoServerAddress"></a> Подключение нового узла к адресу сервера Windows Server Essentials

1.  На начальной странице откройте диспетчер DNS. Чтобы открыть диспетчер DNS, введите в строке поиска **dnsmgmt.msc** и щелкните в результатах **dnsmgmt.msc** .

2.  В дереве консоли диспетчера DNS разверните узел локальный сервер, затем узел **зоны прямого просмотра**, щелкните правой кнопкой мыши зону с суффиксом домена сервера и выберите пункт **новый узел (A или AAAA)**.

3.  Введите имя и IP-адрес сервера (например, DirectAccess-NLS.contoso.local), а также соответствующий адрес сервера (например, 192.168.x.x).

4.  Щелкните **Добавить узел**, после чего нажмите **OK**, а затем — **Готово**.

##  <a name="step-4-create-a-security-group-for-directaccess-client-computers"></a><a name="BKMK_AddSecurityGroup"></a> Шаг 4. Создание группы безопасности для клиентских компьютеров DirectAccess
 Теперь необходимо создать группу безопасности для клиентских компьютеров DirectAccess и добавить в нее учетные записи компьютеров.

#### <a name="to-add-a-security-group-for-client-computers-that-use-directaccess"></a>Создание группы безопасности для клиентских компьютеров, использующих DirectAccess

1. На панели мониторинга диспетчера серверов щелкните **Сервис** и нажмите **Active Directory — пользователи и компьютеры**.

   > [!NOTE]
   >  Если в меню **Сервис** отсутствует пункт **Active Directory — пользователи и компьютеры**, необходимо установить данный компонент. Для этого необходимо выполнить с правами администратора следующий командлет Windows PowerShell: `Install-WindowsFeature RSAT-ADDS-Tools`. Подробную информацию см. в статье [Установка или удаление средств удаленного администрирования сервера](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730825(v=ws.11)).

2. В дереве консоли разверните сервер, щелкните правой кнопкой мыши **Пользователи**, нажмите **Создать** и выберите пункт **Группа**.

3. Укажите имя, область и тип группы (необходимо создать группу безопасности), после чего щелкните **OK**.

   Новая группа безопасности будет добавлена в папку **Пользователи**.

#### <a name="to-add-computer-accounts-to-the-security-group"></a>Добавление учетных записей компьютеров в группу безопасности

1.  На панели мониторинга диспетчера серверов щелкните **Сервис** и нажмите **Active Directory — пользователи и компьютеры**.

2.  В дереве консоли разверните сервер и щелкните **Пользователи**.

3.  В списке учетных записей пользователей и групп безопасности сервера щелкните правой кнопкой мыши созданную вами для DirectAccess группу безопасности и откройте **Свойства**.

4.  На вкладке **Члены группы** щелкните **Добавить**.

5.  В диалоговом окне укажите через точку с запятой (;) имена учетных записей компьютеров, которые вы желаете добавить группу. После этого щелкните **Проверить имена**.

6.  После проверки учетных записей компьютеров щелкните **OK**. Затем повторно нажмите **OK**.

> [!NOTE]
>  Добавить учетную запись в группу безопасности также можно на вкладке **Входит в состав** в свойствах учетной записи компьютера.

##  <a name="step-5-enable-and-configure-directaccess"></a><a name="BKMK_EnableConfigureDA"></a> Шаг 5. Включение и Настройка DirectAccess
 Чтобы включить и настроить DirectAccess в Windows Server Essentials, необходимо выполнить следующие действия.

-   [Шаг 5а. Включение DirectAccess через консоль управления удаленным доступом](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)

-   [Шаг 5b. Удаление недопустимого IPv6Prefix в объекте групповой политики RRAS (только для Windows Server Essentials)](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)

-   [Шаг 5в. Настройка DirectAccess на клиентских компьютерах под управлением Windows 7 Enterprise](#BKMK_Step4cWindows7Setup)

-   [Шаг 5г. Настройка сервера сетевых расположений](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)

-   [Шаг 5д. Добавление раздела реестра для обхода сертификации ЦС при установке канала IPsec](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)

###  <a name="step-5a-enable-directaccess-by-using-the-remote-access-management-console"></a><a name="BKMK_EnableDA"></a> Шаг 5A. Включение DirectAccess с помощью консоли управления удаленным доступом
 В этом разделе приводятся пошаговые инструкции по включению DirectAccess в Windows Server Essentials. Если вы еще не настроили VPN-сервер, необходимо сделать это до выполнения описанных действий. Инструкции см. в разделе [Управление VPN](Manage-VPN-in-Windows-Server-Essentials.md).

##### <a name="to-enable-directaccess-by-using-the-remote-access-management-console"></a>Включение DirectAccess через консоль управления удаленным доступом

1.  На начальной странице откройте меню **Управление удаленным доступом**.

2.  В мастере включения DirectAccess выполните следующие действия.

    1.  Проверьте **Требования для DirectAccess** и щелкните **Далее**.

    2.  На вкладке **Выбор групп** добавьте группу безопасности, созданную вами ранее для клиентов DirectAccess (Если группа безопасности не создана, см. инструкции [в разделе Шаг 4. Создание группы безопасности для клиентских компьютеров DirectAccess](#BKMK_AddSecurityGroup) .)

    3.  На вкладке **Выбор групп** щелкните **Разрешить DirectAccess только для мобильных компьютеров**, если вы хотите разрешить мобильными компьютерам использовать DirectAccess для удаленного доступа к серверу, а затем нажмите кнопку **Далее**.

    4.  На странице **Топология сети** выберите топологию сервера и нажмите кнопку **Далее**.

    5.  На странице **Список DNS-суффиксов** добавьте дополнительный DNS-суффикс для клиентских компьютеров, если это необходимо, и нажмите кнопку **Далее**.

        > [!NOTE]
        >  Мастер DirectAccess по умолчанию добавляет DNS-суффикс текущего домена. При необходимости можно добавить и другие суффиксы.

    6.  Проверьте объекты групповой политики, которые будут применяться, и при необходимости измените их.

    7.  Нажмите кнопку **Далее**, а затем кнопку **Готово**.

    8.  Перезапустите службу управления удаленным доступом, выполнив следующую команду Windows PowerShell в режиме с повышенными правами:

        ```powershell
        Restart-Service RaMgmtSvc
        ```

###  <a name="step-5b-remove-the-invalid-ipv6prefix-in-rras-gpo-windows-server-essentials-only"></a><a name="BKMK_RemoveIPv6"></a> Шаг 5b. Удаление недопустимого IPv6Prefix в объекте групповой политики RRAS (только для Windows Server Essentials)
  Этот раздел относится к серверу, на котором выполняется Windows Server Essentials.

 Откройте Windows PowerShell от имени администратора и выполните следующие команды.

```powershell
gpupdate
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix
gpupdate
```

###  <a name="step-5c-enable-client-computers-running-windows-7-enterprise-to-use-directaccess"></a><a name="BKMK_Step4cWindows7Setup"></a> Шаг 5C. Включение использования DirectAccess клиентскими компьютерами под управлением Windows 7 Корпоративная
 Если у вас есть клиентские компьютеры под управлением Windows 7 Корпоративная, выполните следующую процедуру, чтобы включить DirectAccess с этих компьютеров.

##### <a name="to-enable--windows-7-enterprise-computers-to-use-directaccess"></a>Включение использования DirectAccess компьютерами под управлением Windows 7 Enterprise

1.  На начальной странице сервера откройте **Управление удаленным доступом**.

2.  В консоли управления удаленным доступом щелкните **Конфигурация**. В области **Подробности установки** щелкните **Изменить** для пункта **Шаг 2**.

     Откроется мастер установки сервера удаленного доступа.

3.  На вкладке **Проверка подлинности** выберите сертификат центра сертификации (ЦС), который будет доверенным корневым сертификатом (можно выбрать сертификат ЦС сервера Windows Server Essentials). Щелкните **Разрешить клиентским компьютерам с Windows 7 подключаться с помощью DirectAccess**, после чего нажмите **Далее**.

4.  Для завершения работы мастера следуйте инструкциям на экране.

> [!IMPORTANT]
>  Существует известная ошибка для подключения компьютеров Windows 7 Корпоративная через DirectAccess, если сервер Windows Server Essentials не поставляется с предварительно установленным UR1. Для активации подключений DirectAccess в этой среде необходимы дополнительные действия:
>
> 1. Установите исправление, описанное в [статье базы знаний майкрософт 2796394](https://support.microsoft.com/kb/2796394) на сервере Windows Server Essentials. Перезапустите сервер.
>    2. Затем установите исправление, описанное в [статье 2615847 базы знаний Майкрософт](https://support.microsoft.com/kb/2615847) , на каждом компьютере с Windows 7.
>
>    Эта проблема была решена в Windows Server Essentials.

###  <a name="step-5d-configure-the-network-location-server"></a><a name="BKMK_NLS"></a> Шаг 5D. Настройка сервера сетевых расположений
 Этот раздел содержит поэтапные инструкции по настройке параметров сервера сетевых расположений.

> [!NOTE]
>  Перед началом скопируйте содержимое папки <SystemDrive \> \Inetpub\Wwwroot в папку <systemdrive \> \Program Files\Windows сервер\бин\вебаппс\сите\инсидеаутсиде. Также скопируйте файл Default. aspx из папки <SystemDrive \> \Program Files\Windows сервер\бин\вебаппс\сите в папку <systemdrive \> \Program Files\Windows сервер\бин\вебаппс\сите\инсидеаутсиде.

##### <a name="to-configure-the-network-location-server"></a>Настройка сервера сетевых расположений

1.  На начальной странице откройте меню **Управление удаленным доступом**.

2.  В консоли управления удаленным доступом щелкните **Конфигурация**, после чего в области сведений **Установка удаленного доступа** нажмите **Изменить** для пункта **Шаг 3**.

3.  В мастере установки сервера удаленного доступа на вкладке **Сервер сетевых расположений** выберите **Сервер сетевых расположений развернут на сервере удаленного доступа**, после чего укажите сертификат, выданный в ходе предыдущего шага ( [Step 3: Prepare a certificate and DNS record for the network location server](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)).

4.  Выполните инструкции для завершения работы мастера и нажмите кнопку **Готово**.

###  <a name="step-5e-add-a-registry-key-to-bypass-ca-certification-when-you-establish-an-ipsec-channel"></a><a name="BKMK_CA"></a> Шаг 5e. Добавление раздела реестра для обхода сертификации ЦС при установке канала IPsec
 Теперь вам следует настроить сервер на обход сертификации ЦС при установке канала IPsec.

##### <a name="to-add-a-registry-key-to-bypass-the-ca-certification"></a>Добавление раздела реестра для обхода сертификации ЦС

1.  На начальной странице откройте приложение **regedit** (редактор реестра).

2.  В редакторе реестра перейдите в раздел **HKEY_LOCAL_MACHINE** > **System** > **CurrentControlSet** > **Services** > **IKEEXT**.

3.  В разделе **IKEEXT** щелкните правой кнопкой мыши строку **Parameters**, нажмите **Создать**, после чего выберите **Параметр DWORD (32 бита)**.

4.  Переименуйте созданное значение в **ikeflags**.

5.  Дважды щелкните параметр **ikeflags**, в поле **Система счисления** выберите **Шестнадцатеричная**, задайте значение **8000** и нажмите **OK**.

> [!NOTE]
>  Для добавления этого раздела реестра вы можете использовать следующую команду Windows PowerShell в режиме с повышенными правами:
>
>  `Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000`

##  <a name="step-6-configure-name-resolution-policy-table-settings-for-the-directaccess-server"></a><a name="BKMK_NRPT"></a> Шаг 6. Настройка параметров таблица политики разрешения имен для сервера DirectAccess
 В этом разделе приведены инструкции по изменению записей таблицы политики разрешения имен (NPRT) для внутренних адресов (например, записей с суффиксом contoso.local) для объектов групповой политики клиента DirectAccess, а также по дальнейшей установке адреса интерфейса IPHTTPS.

#### <a name="to-configure-name-resolution-policy-table-entries"></a>Настройка записей таблицы политики разрешения имен

1.  На начальной странице откройте меню **Управление групповыми политиками**.

2.  В консоли управления групповыми политиками щелкните лес и домен по умолчанию, нажмите правой кнопкой мыши **Параметры клиента DirectAccess**, а затем щелкните **Изменить**.

3.  Щелкните **Конфигурации компьютера**, затем **Политики**, нажмите **Конфигурация Windows**, после чего выберите пункт **Политика разрешения имен**. Выберите запись, пространство имен которой идентично вашему DNS-суффиксу, и щелкните **Изменить правило**.

4.  Щелкните вкладку **Параметры DNS для DirectAccess**, затем выберите **Разрешить параметры DNS для DirectAccess в этом правиле**. Добавьте адрес IPv6 для интерфейса IP-HTTPS в список серверов DNS.

    > [!NOTE]
    >  Для получения адреса IPv6 можно использовать следующую команду Windows PowerShell:
    >
    >  `(Get-NetIPInterface -InterfaceAlias IPHTTPSInterface | Get-NetIPAddress -PrefixLength 128)[1].IPAddress`

##  <a name="step-7-configure-tcp-and-udp-firewall-rules-for-the-directaccess-server-gpos"></a><a name="BKMK_TCPUDP"></a> Шаг 7. Настройка правил брандмауэра TCP и UDP для объектов групповой политики сервера DirectAccess
 В этот раздел входят пошаговые инструкции по настройке правил брандмауэра TCP и UDP для объектов групповой политики сервера DirectAccess.

#### <a name="to-configure-firewall-rules"></a>Настройка правил брандмауэра

1.  На начальной странице откройте меню **Управление групповыми политиками**.

2.  В консоли управления групповыми политиками щелкните лес и домен по умолчанию, нажмите правой кнопкой мыши **Параметры сервера DirectAccess**, а затем щелкните **Изменить**.

3.  Перейдите в раздел **Конфигурация компьютера** > **Политики** > **Конфигурация Windows** > **Параметры безопасности** > **Брандмауэр Windows в режиме повышенной безопасности**, после чего перейдите на следующий уровень меню **Брандмауэр Windows в режиме повышенной безопасности** и откройте **Правила для входящих подключений**. Щелкните правой кнопкой мыши **Сервер доменных имен (входящий трафик TCP)** и выберите **Свойства**.

4.  Щелкните вкладку **Область** и в списке **Локальный IP-адрес** добавьте адрес IPv6 интерфейса IP-HTTPS.

5.  Повторите ту же процедуру для **Сервера доменных имен (входящий трафик UDP)**.

##  <a name="step-8-change-the-dns64-configuration-to-listen-to-the-ip-https-interface"></a><a name="BKMK_DNS64"></a> Шаг 8. изменение конфигурации DNS64 для прослушивания интерфейса IP-HTTPS
 Чтобы выполнялось ожидание передачи данных интерфейса IP-HTTPS, конфигурацию DNS64 необходимо изменить при помощи следующей команды Windows PowerShell.

```powershell
Set-NetDnsTransitionConfiguration -AcceptInterface IPHTTPSInterface
```

##  <a name="step-9-reserve-ports-for-the-winnat-service"></a><a name="BKMK_ExemptPort"></a> Шаг 9. резервирование портов для службы WinNat
 Чтобы зарезервировать порты для службы WinNat, используйте следующие команды Windows PowerShell. Замените "192.168.1.100" фактическим IPv4-адресом сервера Windows Server Essentials.

```powershell
Set-NetNatTransitionConfiguration -IPv4AddressPortPool @("192.168.1.100, 10000-47000")
```

> [!IMPORTANT]
>  Во избежание конфликтов с приложениями убедитесь, что в диапазон зарезервированных для службы WinNat портов не входит порт 6602.

##  <a name="step-10-restart-the-winnat-service"></a><a name="BKMK_WinNAT"></a> Шаг 10. перезапуск службы WinNat
 Перезапустите службу драйвера NAT Windows (WinNat) с помощью следующей команды Windows PowerShell.

```powershell
Restart-Service winnat
```

##  <a name="appendix-set-up-directaccess-by-using-windows-powershell"></a><a name="BKMK_AppendixBPowerShellScript"></a> Приложение. Настройка DirectAccess с помощью Windows PowerShell
 Этот раздел описывает установку и настройку DirectAccess с помощью Windows PowerShell.

### <a name="preparation"></a>Подготовка
 Перед началом настройки сервера для DirectAccess необходимо выполнить следующие действия.

1.  Выполните процедуру, описанную в [шаге 3: Подготовка сертификата и записи DNS для сервера сетевого расположения](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS) для регистрации сертификата с именем **DirectAccess-NLS.contoso.com** (где **contoso.com** заменяется фактическим внутренним именем домена) и добавьте запись DNS для сервера сетевого расположения (NLS).

2.  Добавьте группу безопасности под названием **DirectAccessClients** в Active Directory, а затем добавьте клиентские компьютеры, которым следует предоставить доступ к функциям DirectAccess. Дополнительные сведения см. в разделе [Шаг 4. Создание группы безопасности для клиентских компьютеров DirectAccess](#BKMK_AddSecurityGroup).

### <a name="commands"></a>Команды

> [!IMPORTANT]
>  В Windows Server Essentials нет необходимости удалять ненужный объект групповой политики префикса IPv6. Удалите раздел кода со следующей меткой: `# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO`.

```powershell
# Add Remote Access role if not installed yet
$ra = Get-WindowsFeature RemoteAccess
If ($ra.Installed -eq $FALSE) { Add-WindowsFeature RemoteAccess }

# Server may need to restart if you installed RemoteAccess role in the above step

# Set the internet domain name to access server, replace contoso.com below with your own domain name
$InternetDomain = "www.contoso.com"
#Set the SG name which you create for DA clients
$DaSecurityGroup = "DirectAccessClients"
#Set the internal domain name
$InternalDomain = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().Name

# Set static IP and DNS settings
$NetConfig = Get-WmiObject Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true"
$CurrentIP = $NetConfig.IPAddress[0]
$SubnetMask = $NetConfig.IPSubnet | Where-Object{$_ -like "*.*.*.*"}
$NetConfig.EnableStatic($CurrentIP, $SubnetMask)
$NetConfig.SetGateways($NetConfig.DefaultIPGateway)
$NetConfig.SetDNSServerSearchOrder($CurrentIP)

# Get physical adapter name and the certificate for NLS server
$Adapter = (Get-WmiObject -Class Win32_NetworkAdapter -Filter "NetEnabled=$true").NetConnectionId
$Certs = dir cert:\LocalMachine\My
$nlscert = $certs | Where-Object{$_.Subject -like "*CN=DirectAccess-NLS*"}

# Add regkey to bypass CA cert for IPsec authentication
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000

# Install DirectAccess.
Install-RemoteAccess -NoPrerequisite -DAInstallType FullInstall -InternetInterface $Adapter -InternalInterface $Adapter -ConnectToAddress $InternetDomain -nlscertificate $nlscert -force

#Restart Remote Access Management service
Restart-Service RaMgmtSvc

# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO

gpupdate
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix
gpupdate

# Enable client computers running Windows 7 to use DirectAccess
$allcertsinroot = dir cert:\LocalMachine\root
$rootcert = $allcertsinroot | Where-Object{$_.Subject -like "*-CAA*"}
Set-DAServer -IPSecRootCertificate $rootcert[0]
Set -DAClient -OnlyRemoteComputers Disabled -Downlevel Enabled

#Set the appropriate security group used for DA client computers. Replace the group name below with the one you created for DA clients
Add-DAClient -SecurityGroupNameList $DaSecurityGroup
Remove-DAClient -SecurityGroupNameList "Domain Computers"

# Gather DNS64 IP address information
$Remoteaccess = get-remoteaccess
$IPinterface = get-netipinterface -InterfaceAlias IPHTTPSInterface | get-netipaddress -PrefixLength 128
$DNS64IP=$IPInterface[1].IPaddress
$Natconfig = Get-NetNatTransitionConfiguration

# Configure TCP and UDP firewall rules for the DirectAccess server GPO
$GpoName = 'GPO:'+$InternalDomain+'\DirectAccess Server Settings'
Get-NetFirewallRule -PolicyStore $GpoName -Displayname "Domain Name Server (TCP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP
Get-NetFirewallrule -PolicyStore $GpoName -Displayname "Domain Name Server (UDP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP

# Configure the name resolution policy settings for the DirectAccess server, replace the DNS suffix below with the one in your domain
$Suffix = '.' + $InternalDomain
set-daclientdnsconfiguration -DNSsuffix $Suffix -DNSIPAddress $DNS64IP

# Change the DNS64 configuration to listen to IP-HTTPS interface
Set-NetDnsTransitionConfiguration -AcceptInterface IPHTTPSInterface

# Copy the necessary files to NLS site folder
XCOPY 'C:\inetpub\wwwroot' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /E /Y
XCOPY 'C:\Program Files\Windows Server\Bin\WebApps\Site\Default.aspx' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /Y

# Reserve ports for the WinNat service
Set-NetNatTransitionConfiguration -IPv4AddressPortPool @("192.168.1.100, 10000-47000")

# Restart the WinNat service
Restart-Service winnat
```

## <a name="additional-references"></a>Дополнительные ссылки

-   [Управление повсеместным доступом](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Управление Windows Server Essentials](Manage-Windows-Server-Essentials.md)