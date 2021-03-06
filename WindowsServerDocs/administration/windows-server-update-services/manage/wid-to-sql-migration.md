---
title: Миграция базы данных WSUS из (внутренняя база данных Windows) WID в SQL
description: Раздел о службе Windows Server Update Service (WSUS). Перенос базы данных WSUS (SUSDB) из экземпляра внутренней базы данных Windows в локальный или удаленный экземпляр SQL Server.
ms.topic: how-to
ms.assetid: 90e3464c-49d8-4861-96db-ee6f8a09g7dr
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 07/25/2018
ms.openlocfilehash: 5635f3730ee5a22496558393014d5880d1ab8fba
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101827241"
---
# <a name="migrating-the-wsus-database-from-wid-to-sql"></a>Миграция базы данных WSUS из WID в SQL

> Область применения: Windows Server 2012, Windows Server 2012 R2, Windows Server 2016

Выполните следующие действия, чтобы перенести базу данных WSUS (SUSDB) из экземпляра внутренней базы данных Windows на локальный или удаленный экземпляр SQL Server.

## <a name="prerequisites"></a>Предварительные требования

- Экземпляр SQL. Это может быть **MSSQLServer** или пользовательский экземпляр по умолчанию.
- SQL Server Management Studio.
- WSUS с установленной ролью WID
- IIS (обычно это включается при установке WSUS с помощью диспетчер сервера). Она еще не установлена, она должна быть.

## <a name="migrating-the-wsus-database"></a>Миграция базы данных WSUS

### <a name="stop-the-iis-and-wsus-services-on-the-wsus-server"></a>Останавливает службы IIS и WSUS на сервере WSUS

В PowerShell (с повышенными правами) выполните:

```powershell
    Stop-Service IISADMIN
    Stop-Service WsusService
```

### <a name="detach-susdb-from-the-windows-internal-database"></a>Отсоединение SUSDB от внутренней базы данных Windows

#### <a name="using-sql-management-studio"></a>Использование SQL Management Studio

1. Щелкните правой кнопкой мыши **SUSDB** - &gt; **задачи** и - &gt; выберите пункт **отсоединить**: ![ снимок экрана SQL Server Management Studio отображения задач SUSDB > задачи > отсоединить.](images/image1.png)
2. Установите флажок **Удалить существующие подключения** и нажмите кнопку **ОК** (необязательно, если существуют активные соединения).
    ![Снимок экрана: диалоговое окно "Отсоединение базы данных" с выбранным параметром "удалить существующие соединения" и выделенным параметром "ОК".](images/image2.png)

#### <a name="using-command-prompt"></a>Использование командной строки

> [!IMPORTANT]
> В этих шагах показано, как отключить базу данных WSUS (SUSDB) из экземпляра внутренней базы данных Windows с помощью программы **sqlcmd** . Дополнительные сведения о программе **sqlcmd** см. в разделе [программа sqlcmd](https://go.microsoft.com/fwlink/?LinkId=81183).
> 1. Откройте командную строку с повышенными привилегиями
> 2. Выполните следующую команду SQL, чтобы отключить базу данных WSUS (SUSDB) из экземпляра внутренней базы данных Windows с помощью программы **sqlcmd** :

```batchfile
        sqlcmd -S \\.\pipe\Microsoft##WID\tsql\query
        use master
        GO
        alter database SUSDB set single_user with rollback immediate
        GO
        sp_detach_db SUSDB
        GO
```

### <a name="copy-the-susdb-files-to-the-sql-server"></a>Скопируйте файлы SUSDB в SQL Server

1. Скопируйте **SUSDB. mdf** и **SUSDB \_ log. ldf** из папки данных WID (**% systemdrive%** \\ **данных Windows \\ WID \\**) в папку данных экземпляра SQL.

> [!TIP]
> Например, если папка экземпляра SQL — **C:\Program FILES\MICROSOFT SQL Server\MSSQL12. МССКЛСЕРВЕР\МССКЛ**, а папка данных WID — **к:\виндовс\вид\дата,** скопируйте файлы SUSDB из **К:\виндовс\вид\дата** в папку **C:\Program Files\Microsoft SQL Server\MSSQL12. Мссклсервер\мсскл\дата**

### <a name="attach-susdb-to-the-sql-instance"></a>Присоединение SUSDB к экземпляру SQL

1. В **SQL Server Management Studio** в узле **экземпляр** щелкните правой кнопкой мыши узел **базы данных** и выберите команду **присоединить**.
    ![Снимок экрана SQL Server Management Studio с выбранным параметром "присоединить > базы данных".](images/image3.png)
2. В поле **Присоединение баз данных** в разделе **базы данных для присоединения** нажмите кнопку **добавить** , найдите файл **SUSDB. mdf** (скопированный из папки WID) и нажмите кнопку **ОК**.
    ![Снимок экрана: диалоговое окно "присоединение баз данных" с выделенным параметром "Добавить".](images/image4.png)
    ![Снимок экрана: диалоговое окно "размещение файлов базы данных" с выделенным файлом S U d B D F.](images/image5.png)

> [!TIP]
> Это также можно сделать с помощью Transact-SQL.  Дополнительные сведения о [присоединении базы данных](/sql/relational-databases/databases/attach-a-database) см. в документации по SQL.
>
> Пример (использование путей из предыдущего примера):
> ```sql
>    USE master;
>    GO
>    CREATE DATABASE SUSDB
>    ON
>        (FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data\SUSDB.mdf'),
>        (FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log\SUSDB_Log.ldf')
>        FOR ATTACH;
>    GO
>```

### <a name="verify-sql-server-and-database-logins-and-permissions"></a>Проверка SQL Server и имен входа и разрешений базы данных

#### <a name="sql-server-login-permissions"></a>SQL Server разрешения для входа

После подключения SUSDB убедитесь, что **NT Authority\Network Service** имеет разрешения на вход в экземпляр SQL Server, выполнив следующие действия.

1. Переход к SQL Server Management Studio
2. Открытие экземпляра
3. Щелкните **Безопасность** .
4. Щелкните **имена входа**

Должна быть указана учетная запись **NT Authority\Network Service** . Если это не так, необходимо добавить новое имя для входа.

> [!IMPORTANT]
> Если экземпляр SQL находится на другом компьютере из служб WSUS, учетная запись компьютера сервера WSUS должна быть указана в формате **[FQDN] \\ [всускомпутернаме] $**.  В противном случае можно использовать приведенные ниже шаги, чтобы добавить его, заменив **NT Authority\Network Service** учетной записью компьютера сервера WSUS (**[FQDN] \\ [всускомпутернаме] $**) это будет **_Дополнительно к_*_ предоставлению прав на _* NT Authority\Network Service** .

##### <a name="adding-nt-authoritynetwork-service-and-granting-it-rights"></a>Добавление NT AUTHORITY\NETWORK SERVICE и предоставление ей прав доступа

1. Щелкните правой кнопкой мыши **имена входа** и выберите **создать имя входа...**
    ![Снимок экрана SQL Server Management Studio с выбранным параметром имена входа > новый вход.](images/image6.png)
2. На странице **Общие** введите **имя входа** (**NT Authority\Network Service**) и задайте для **базы данных по умолчанию** значение SUSDB.
    ![Снимок экрана: страница "Общие" диалогового окна "вход" с заполненными полями "имя входа" и "база данных Дефуалт".](images/image7.png)
3. На странице **роли сервера** убедитесь, что выбраны **Общие** и **sysadmin** .
    ![Снимок экрана: страница "роли сервера" диалогового окна входа с выбранными параметрами "общедоступный" и "sysadmin".](images/image8.png)
4. На странице **Сопоставление пользователей** :
    - В разделе **Пользователи, сопоставленные с этим именем входа** выберите **SUSDB** .
    - В разделе **членство в роли базы данных для: SUSDB** убедитесь, что установлены следующие флажки:
        - **public**
        - **WebService** ![ Снимок экрана: страница "Сопоставление пользователей" диалогового окна "вход" с выбранными параметрами "общедоступные" и "веб-служба".](images/image9.png)
5. Нажмите кнопку **ОК**.

Теперь в разделе имена входа будет отображаться **NT Authority\Network Service** .
![Снимок экрана: в обозревателе объектов отображается СЕТЕВая служба "N T AUTHORITY" в разделе "имена входа".](images/image10.png)

#### <a name="database-permissions"></a>Разрешения базы данных

1. Щелкните правой кнопкой мыши SUSDB
2. Выберите пункт **Свойства**.
3. Щелкните **разрешения** .

Должна быть указана учетная запись **NT Authority\Network Service** .

1. Если это не так, добавьте учетную запись.
2. В текстовом поле Login name (имя входа) введите компьютер WSUS в следующем формате:
    > [**Полное доменное имя] \\ [Всускомпутернаме] $**
3. Убедитесь, что для **базы данных по умолчанию** задано значение **SUSDB**.

    > [!TIP]
    > В следующем примере полное доменное имя — **Contosto.com** , а имя машины WSUS — **всусмачине**:
    >
    > ![Снимок экрана: диалоговое окно входа, показывающее, что полное доменное имя — Contosto.com * *, а имя компьютера W s U s — W s u s.](images/image11.png)

4. На странице **Сопоставление пользователей** выберите базу данных **SUSDB** в разделе **Пользователи, сопоставленные с этим именем входа** .
5. Проверьте веб- **службу** в разделе **членство в роли базы данных для: SUSDB**:  ![ снимок экрана страницы сопоставление пользователей диалогового окна имя входа, в котором отображаются выбранные параметры SUSDB и WebService.](images/image12.png)
6. Нажмите кнопку  **ОК** , чтобы сохранить параметры.
    > [!NOTE]
    > Чтобы изменения вступили в силу, может потребоваться перезапустить службу SQL.

### <a name="edit-the-registry-to-point-wsus-to-the-sql-server-instance"></a>Измените реестр, чтобы указать WSUS на экземпляр SQL Server

> [!IMPORTANT]
> Внимательно выполните действия, описанные в этом разделе. Неправильное изменение реестра может привести к серьезным проблемам. Перед внесением изменений [создайте резервную копию реестра для его восстановления](https://support.microsoft.com/help/322756) в случае возникновения проблем.

1. Нажмите кнопку **Пуск**, выберите пункт **Выполнить**, введите **regedit** и нажмите кнопку **ОК**.
2. Откройте следующий раздел: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\UpdateServices\Server\Setup\SqlServerName**
3. В текстовом поле **значение** введите **[SERVERNAME] \\ [имя_экземпляра]** и нажмите кнопку **ОК**. Если имя экземпляра является экземпляром по умолчанию, введите **[SERVERNAME]**.
4. Откройте следующий раздел: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Update Services\Server\Setup\Installed Role Services\UpdateServices-WidDatabase** ![ снимке экрана диалогового окна Редактор реестра с выделенным UpdateServices-WidDatabaseным ключом.](images/image13.png)
5. Переименование раздела **UpdateServices-Database** ![ снимка экрана в диалоговом окне редактора реестра, отображающего обновление имени ключа в UpdateServices-Database.](images/image14.png)

    > [!NOTE]
    > Если не обновить этот ключ, **WsusUtil** попытается обслуживать WID, а не экземпляр SQL, с которым был осуществлен перенос.

### <a name="start-the-iis-and-wsus-services-on-the-wsus-server"></a>Запуск служб IIS и WSUS на сервере WSUS

В PowerShell (с повышенными правами) выполните:

```powershell
    Start-Service IISADMIN
    Start-Service WsusService
```

> [!NOTE]
> Если вы используете консоль WSUS, закройте и перезапустите ее.

## <a name="uninstalling-the-wid-role-not-recommended"></a>Удаление роли WID (не рекомендуется)

> [!WARNING]
> При удалении роли WID также удаляется папка базы данных (**%systemdrive%\Program Files\Update сервицес\датабасе**), содержащая скрипты, необходимые WSUSUtil.exe для выполнения задач, выполняемых после установки. Если вы решили удалить роль WID, убедитесь, что создана резервная копия папки **%systemdrive%\Program Files\Update сервицес\датабасе** .

С помощью PowerShell:

```powershell
Uninstall-WindowsFeature -Name 'Windows-Internal-Database'
```

После удаления роли WID убедитесь в наличии следующего раздела реестра: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Update Services\Server\Setup\Installed Role Services\UpdateServices-Database**