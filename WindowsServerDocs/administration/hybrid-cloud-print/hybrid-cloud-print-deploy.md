---
title: Развертывание функции Hybrid Cloud Print в Windows Server
description: Настройка гибридной облачной печати (Майкрософт)
ms.assetid: fc239aec-e719-47ea-92fc-d82a7247c5e9
ms.topic: how-to
author: msjimwu
ms.author: coreyp
manager: dongill
ms.date: 3/15/2018
ms.openlocfilehash: 3e5b732beb502bb0bf365136947ff380caf71545
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879915"
---
# <a name="deploy-windows-server-hybrid-cloud-print"></a>Развертывание функции Hybrid Cloud Print в Windows Server

>Область применения. Windows Server 2016

В этой статье для ИТ-администраторов описывается комплексное развертывание решения Microsoft гибридного облака (HCP). Эти уровни решений поверх существующих серверов Windows Server, работающих в качестве сервера печати, и обеспечивают присоединение Azure Active Directory (Azure AD) и управляемые MDM, устройства для обнаружения и печати на управляемых принтерах Организации.

## <a name="pre-requisites"></a>Предварительные требования

Перед началом установки необходимо получить несколько подписок, служб и компьютеров. Вот они:

- Подписка Azure AD Premium.

  См. статью [Начало работы с подпиской Azure](https://azure.microsoft.com/trial/get-started-active-directory/) для пробной подписки в Azure.

- Служба MDM, например Intune.

  См. статью [Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) для пробной подписки на Intune.

- Компьютер под Active Directory Windows Server 2016 или более поздней версии.

  Дополнительные сведения о настройке Active Directory см. [в статье Пошаговое руководство. настройка Active Directory в Windows Server 2016](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/) .

- Выделенный, присоединенный к домену компьютер Windows Server 2016 или более поздней версии, работающий как сервер печати.

- Выделенный, присоединенный к домену компьютер Windows Server 2016 или более поздней версии, работающий как сервер соединителя.

  Дополнительные сведения см. в статье [Знакомство с соединителями Azure AD application proxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors) .

- Для публикации принтеров в Windows 10 имеется обновление или более поздний компьютер.

- Общедоступное доменное имя.

  Вы можете использовать имя домена, созданное Azure (*имя_домена*. onmicrosoft.com), или приобрести собственное доменное имя. См. раздел [Добавление имени личного домена с помощью портала Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/add-custom-domain).

## <a name="deployment-steps"></a>Шаги по развертыванию

Приведенные ниже шаги предназначены для типичного гибридного развертывания для печати в облаке.

### <a name="step-1---install-azure-ad-connect"></a>Шаг 1. Установка Azure AD Connect

1. Azure AD Connect синхронизирует Azure AD с локальной службой AD. На компьютере Windows Server с Active Directory Скачайте и установите Azure AD Connect программное обеспечение с помощью стандартных параметров. См. раздел [Приступая к работе с Azure AD Connect с помощью стандартных параметров](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-express).

### <a name="step-2---install-application-proxy"></a>Шаг 2. Установка прокси приложения

1. Прокси приложения позволяет пользователям в вашей организации получать доступ к локальным приложениям из облака. Установите прокси приложения на сервере соединителя.
    - Инструкции по установке см. [в разделе Учебник. Добавление локального приложения для удаленного доступа через прокси приложения в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-add-on-premises-application).
    - Если организация имеет сложную топологию сети, рекомендуется использовать выделенную группу соединителей. См. раздел [Публикация приложений в отдельных сетях и расположениях с помощью групп соединителей](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connector-groups).

### <a name="step-3---register-and-configure-applications"></a>Шаг 3. Регистрация и настройка приложений

Чтобы включить проверку подлинности при взаимодействии со службами HCP, необходимо создать 3 приложения: 2 веб-приложения для представления двух служб HCP и 1 собственное приложение для взаимодействия с этими службами.

1. Войдите в портал Azure, чтобы зарегистрировать веб-приложения.
    - В разделе Azure Active Directory выберите **Регистрация приложений**  >  **Новая регистрация**.

    ![Регистрация приложения AAD 1](../media/hybrid-cloud-print/AAD-AppRegistration.png)

    - Введите имя приложения для службы обнаружения Mopria. Нажмите кнопку **Регистрация** для завершения.

    ![Регистрация приложения AAD 2](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria.png)

    - Повторите процедуру для корпоративной облачной службы печати.
    - Повторите процедуру для собственного приложения.
    - Три приложения должны отображаться в разделе **Регистрация приложений**.

    ![Регистрация приложения AAD 3](../media/hybrid-cloud-print/AAD-AppRegistration-AllApps.png)

2. Предоставление API для 2 веб-приложений.
    - Находясь в колонке **Регистрация приложений** , щелкните приложение службы обнаружения Mopria, выберите **предоставить API**, а затем щелкните **задать** рядом с URI идентификатора приложения.

    ![Функция AAD предоставляет API 1](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI.png)

    - Щелкните **сохранить** , не изменяя значение по умолчанию для URI идентификатора приложения. Это значение нужно установить сейчас, и оно будет изменено позже.

    ![Интерфейс AAD предоставляет API 2](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-Save.png)

    - Щелкните **Добавить область**.

    ![Интерфейс AAD предоставляет API 3](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-AddScope.png)

    - Укажите имя области, разрешите как администраторам, так и пользователям согласие, введите описание согласия, а затем щелкните **Добавить область** для завершения.

    ![Интерфейс AAD предоставляет API 4](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-ScopeName.png)

    - Повторите процедуру для корпоративной облачной службы печати. Используйте другое имя области и описание согласия.

    ![Интерфейс AAD предоставляет API 5](../media/hybrid-cloud-print/AAD-AppRegistration-ECP-ExposeAPI-ScopeName.png)

3. Добавление разрешений API
    - Вернитесь в колонку Регистрация приложений. Щелкните собственное приложение и выберите разрешения API. Щелкните **Добавить разрешение**.

    ![Разрешение API AAD 1](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission.png)

    - Переключитесь на **API, используемые моей организацией**, а затем используйте поле поиска, чтобы найти службу Mopria Discovery, добавленную ранее. Щелкните службу в результатах поиска.

    ![Разрешение API AAD 2](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Mopria.png)

    - Выберите **делегированные разрешения**. Установите флажок рядом с областью API. Щелкните **Добавить разрешения**.

    ![Разрешение API AAD 3](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Mopria-Add.png)

    - Повторите, чтобы добавить разрешения для корпоративной облачной службы печати.

    ![Разрешение API AAD 4](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-ECP-Add.png)

    - После возврата в колонку разрешения API подождите 10 секунд, прежде чем щелкнуть **согласие общего администратора..**..

    ![Разрешение API AAD 5](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-GrantConsent.png)

    - При появлении запроса нажмите кнопку **Да** .

    ![Разрешение API AAD 6](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-GrantConsent-Yes.png)

    - Убедитесь, что в столбце Состояние разрешения API отображается зеленый флажок.

    ![Разрешение API AAD 7](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Verify.png)

4. Настройка прокси приложения для веб-приложений
    - Перейдите в раздел **Azure Active Directory**  >  **корпоративные приложения**  >  **все приложения**. Найдите службу Mopria Discovery и щелкните ее.

    ![Прокси-сервер приложения AAD 1](../media/hybrid-cloud-print/AAD-EnterpriseApp-AllApps.png)

    - Щелкните **прокси приложения**. Введите внутренний URL-адрес в формате `https://<fully qualified domain name of the Print Server>/mcs/` . Чтобы завершить, нажмите кнопку **сохранить** .

    ![Прокси-сервер приложения AAD 2](../media/hybrid-cloud-print/AAD-EnterpriseApp-Mopria-AppProxy.png)

    - Повторите процедуру для корпоративной облачной службы печати. Обратите внимание, что внутренний URL-адрес — `https://<fully qualified domain name of the Print Server>/ecp/` .

    ![Прокси-сервер приложения AAD 3](../media/hybrid-cloud-print/AAD-EnterpriseApp-ECP-AppProxy.png)

    - Перейдите в **Azure Active Directory**  >  **Регистрация приложений**. Щелкните службу Mopria Discovery. Обратите внимание, что в разделе **Обзор**URI идентификатора приложения был изменен с по умолчанию на внешний URL-адрес в разделе **прокси приложения**. Универсальный код ресурса (URI) будет использоваться во время установки сервера печати, в клиентской политике MDM и для публикации принтера.

    ![Прокси-сервер приложения AAD 4](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-Overview.png)

5. Назначение пользователей для приложений
    - Перейдите в раздел **Azure Active Directory**  >  **корпоративные приложения**  >  **все приложения**. Найдите службу Mopria Discovery и щелкните ее.
    - Щелкните " **Пользователи и группы** " и назначьте пользователей или щелкните " **свойства** " и измените " **требуется назначение пользователей** " **No** ?
    - Повторите процедуру для корпоративной облачной службы печати.

6. Настройка URI перенаправления в собственном приложении
    - Перейдите в **Azure Active Directory**  >  **Регистрация приложений**. Щелкните собственное приложение. Перейдите к разделу **Обзор** и скопируйте **идентификатор приложения (клиента)**.

    ![URI перенаправления AAD 1](../media/hybrid-cloud-print/AAD-AppRegistration-Native-Overview.png)

    - Перейдите к разделу **Проверка подлинности**. Измените раскрывающийся список **тип** на `Public...` и введите два URI перенаправления, используя следующий формат, где `<NativeClientAppID>` — из предыдущего шага:

        `ms-appx-web://Microsoft.AAD.BrokerPlugin/<NativeClientAppID>`

        `ms-appx-web://Microsoft.AAD.BrokerPlugin/S-1-15-2-3784861210-599250757-1266852909-3189164077-45880155-1246692841-283550366`

    ![URI перенаправления AAD 2](../media/hybrid-cloud-print/AAD-AppRegistration-Native-Authentication.png)

    - Чтобы завершить, нажмите кнопку **сохранить** .

### <a name="step-4---setup-the-print-server"></a>Шаг 4. Настройка сервера печати

1. Убедитесь, что на сервере печати установлены все доступные Центр обновления Windows. Примечание. сервер 2019 должен быть исправлен для сборки 17763,165 или более поздней версии.
    - Установите следующие роли сервера:
        - Роль сервера печати
        - Службы IIS
    - Дополнительные сведения об установке ролей сервера см. в [статье Установка ролей, служб ролей и компонентов с помощью мастера добавления ролей и](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installarfw) компонентов.

    ![Роли сервера печати](../media/hybrid-cloud-print/PrintServer-Roles.png)

2. Установите модули PowerShell для гибридной облачной печати.
    - Выполните следующие команды из командной строки PowerShell с повышенными привилегиями:

        `find-module -Name PublishCloudPrinter`чтобы убедиться, что компьютер может достичь коллекция PowerShell (PSGallery)

        `install-module -Name PublishCloudPrinter`

    > Примечание. Вы можете увидеть обмен сообщениями о том, что "PSGallery" является недоверенным репозиторием.  Введите "y", чтобы продолжить установку.

    ![Публикация сервера печати в облачном принтере](../media/hybrid-cloud-print/PrintServer-PublishCloudPrinter.png)

3. Установите гибридное облачное решение для печати.
    - В той же командной строке PowerShell с повышенными привилегиями измените каталог на один из приведенных ниже (требуются кавычки):

        `C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0`

    - Выполнить

        `.\CloudPrintDeploy.ps1 -AzureTenant <Azure Active Directory domain name> -AzureTenantGuid <Azure Active Directory ID>`

    - Чтобы найти Azure Active Directory доменное имя, обратитесь к снимку экрана ниже.

    ![Сервер печати как получить доменное имя AAD](../media/hybrid-cloud-print/PrintServer-GetAADDomainName.png)

    - Чтобы найти идентификатор Azure Active Directory, см. снимок экрана ниже.

    ![Развертывание сервера печати в облаке](../media/hybrid-cloud-print/PrintServer-GetAADId.png)

    - Выходные данные скрипта Клаудпринтдеплой выглядят следующим образом:

    ![Развертывание сервера печати в облаке](../media/hybrid-cloud-print/PrintServer-CloudPrintDeploy.png)

    - Проверьте файл журнала, чтобы узнать, есть ли какие-либо ошибки:`C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0\CloudPrintDeploy.log`

4. Запустите **регитедит** в командной строке с повышенными привилегиями. К компьютеру \ HKEY_LOCAL_MACHINE \Софтваре\микрософт\виндовс\куррентверсион\клаудпринт\ентерприсеклаудпринтсервице.
    - Убедитесь, что для Азуреаудиенце задан универсальный код ресурса (URI) идентификатора приложения облачного приложения для печати в облаке.
    - Убедитесь, что для Азуретенант задано имя домена Azure AD.

    ![Разделы реестра сервера печати ECP](../media/hybrid-cloud-print/PrintServer-RegEdit-ECP.png)

5. К компьютеру \ HKEY_LOCAL_MACHINE \Софтваре\микрософт\виндовс\куррентверсион\клаудпринт\моприадисковерисервице.
    - Убедитесь, что Азуреаудиенце является URI идентификатора приложения для приложения службы обнаружения Mopria.
    - Убедитесь, что Азуретенант является доменным именем Azure AD.
    - Убедитесь, что URL-адрес — это URI идентификатора приложения для приложения службы Mopria Discovery.

    ![Разделы реестра сервера печати Mopria](../media/hybrid-cloud-print/PrintServer-RegEdit-Mopria.png)

6. Запустите **iisreset** в командной строке PowerShell с повышенными привилегиями. Это обеспечит вступление в силу всех изменений, внесенных в реестр на предыдущем шаге.

7. Настройте конечные точки IIS для поддержки SSL.
    - SSL-сертификат может представлять собой самозаверяющий сертификат или один, выданный доверенным центром сертификации (ЦС).
    - При использовании самозаверяющего сертификата **Убедитесь, что сертификат импортирован на клиентские компьютеры**.
    - При регистрации домена с сторонним поставщиком необходимо настроить конечные точки IIS с SSL-сертификатом. Подробные сведения см. в этом [руководству](https://www.sslsupportdesk.com/microsoft-server-2016-iis-10-10-5-ssl-installation/) .

8. Установите пакет SQLite.
   - Откройте командную строку PowerShell с повышенными привилегиями.
   - Выполните следующую команду, чтобы скачать пакеты NuGet System. Data. SQLite.

        `Register-PackageSource -Name nuget.org -ProviderName NuGet -Location https://www.nuget.org/api/v2/ -Trusted -Force`

   - Выполните следующую команду, чтобы установить пакеты.

        `Install-Package system.data.sqlite [-requiredversion x.x.x.x] -providername nuget`

   > Примечание. рекомендуется загрузить и установить последнюю версию, выполнив параметр-requiredversion.

    ![Разделы реестра сервера печати Mopria](../media/hybrid-cloud-print/PrintServer-InstallSQLite.png)

9. Скопируйте библиотеки DLL SQLite в папку Моприаклаудсервице webapp bin (К:\инетпуб\ввврут\моприаклаудсервице\бин).
    - Создайте файл PS1, содержащий сценарий PowerShell, приведенный ниже.
    - Измените переменную $version на версию SQLite, установленную на предыдущем шаге.
    - Запустите PS1 файл в командной строке PowerShell с повышенными привилегиями.

    ```powershell
    $source = \Program Files\PackageManagement\NuGet\Packages
    $core = System.Data.SQLite.Core
    $linq = System.Data.SQLite.Linq
    $ef6 = System.Data.SQLite.EF6
    $version = x.x.x.x
    $target = C:\inetpub\wwwroot\MopriaCloudService\bin

    xcopy /y $source\$core.$version\lib\net46\System.Data.SQLite.dll $target\
    xcopy /y $source\$core.$version\build\net46\x86\SQLite.Interop.dll $target\x86\
    xcopy /y $source\$core.$version\build\net46\x64\SQLite.Interop.dll $target\x64\
    xcopy /y $source\$linq.$version\lib\net46\System.Data.SQLite.Linq.dll $target\
    xcopy /y $source\$ef6.$version\lib\net46\System.Data.SQLite.EF6.dll $target\
    ```

10. Обновите файл c:\inetpub\wwwroot\MopriaCloudService\web.config для включения SQLite версии x. x. x. x в следующих `<runtime>/<assemblyBinding>` разделах. Это та же версия, которая использовалась на предыдущем шаге.

    ```xml
    ...
    <dependentAssembly>
    assemblyIdentity name=System.Data.SQLite culture=neutral publicKeyToken=db937bc2d44ff139 /
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    <dependentAssembly>
    <assemblyIdentity name=System.Data.SQLite.Core culture=neutral publicKeyToken=db937bc2d44ff139 />
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    <dependentAssembly>
    <assemblyIdentity name=System.Data.SQLite.EF6 culture=neutral publicKeyToken=db937bc2d44ff139 />
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    <dependentAssembly>
    <assemblyIdentity name=System.Data.SQLite.Linq culture=neutral publicKeyToken=db937bc2d44ff139 />
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    ...
    ```

11. Создайте базу данных SQLite.
    - Скачайте и установите двоичные файлы средств SQLite из `https://www.sqlite.org/` .
    - Перейдите в `c:\inetpub\wwwroot\MopriaCloudService\Database` каталог.
    - Выполните следующую команду, чтобы создать базу данных в этом каталоге:

        `sqlite3.exe MopriaDeviceDb.db .read MopriaSQLiteDb.sql`

    - В проводнике откройте свойства файла Моприадевицедб. DB, чтобы добавить пользователей или группы, которым разрешено публиковать в базе данных Mopria на вкладке Безопасность. Пользователи или группы должны существовать в локальной Active Directory и синхронизироваться с Azure AD.
    - Если решение развертывается в домене, не поддерживающем маршрутизацию (например, *mydomain*. local), домен Azure AD (например, *имя_домена*. onmicrosoft.com или приобретенный от стороннего поставщика) необходимо добавить в качестве суффикса имени участника-пользователя в локальную Active Directory. Это так же, как пользователь, который будет публиковать принтеры (например admin@*имя_домена*. onmicrosoft.com), можно добавить в параметр безопасности файла базы данных. См. статью [Подготовка домена без поддержки маршрутизации для синхронизации каталогов](https://docs.microsoft.com/office365/enterprise/prepare-a-non-routable-domain-for-directory-synchronization).

    ![Разделы реестра сервера печати Mopria](../media/hybrid-cloud-print/PrintServer-SQLiteDB.png)

### <a name="step-5-optional---configure-pre-authentication-with-azure-ad"></a>Шаг 5 \[ необязательный. \] Настройка предварительной проверки подлинности в Azure AD

1. Проверьте документ [ограниченное делегирование Kerberos для единого входа в приложения с помощью прокси приложения](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-configure-single-sign-on-with-kcd).

2. Настройка локального Active Directory.
    - На Active Directory компьютере откройте диспетчер сервера и выберите **инструменты**  >  **Active Directory пользователи и компьютеры**.
    - Перейдите к узлу **Компьютеры** и выберите сервер соединителя.
    - Щелкните правой кнопкой мыши и выберите **Свойства**  ->  **Делегирование**   .
    - Выберите **доверять компьютеру делегирование указанных служб**.
    - Выберите **использовать любой протокол проверки подлинности**.
    - В разделе **службы, в которых эта учетная запись может представлять делегированные учетные данные**.
        - Добавьте имя участника-службы (SPN) компьютера сервера печати.
        - Выберите узел для типа службы.
    ![Делегирование Active Directory](../media/hybrid-cloud-print/AD-Delegation.png)

3. Убедитесь, что в службах IIS включена проверка подлинности Windows.
    - На сервере печати откройте диспетчер сервера средства > > Диспетчер служб IIS.
    - Перейдите на сайт.
    - Дважды щелкните **Проверка подлинности**.
    - Щелкните **Проверка подлинности Windows** и щелкните **включить** в разделе **действия**.
    ![Проверка подлинности IIS сервера печати](../media/hybrid-cloud-print/PrintServer-IIS-Authentication.png)

4. Настройка единого входа.
    - На портал Azure перейдите в раздел **Azure Active Directory**  >  **корпоративные приложения**  >  **все приложения**.
    - Выберите приложение Моприадисковерисервице.
    - Перейдите на страницу **прокси приложения**. Измените метод предварительной проверки подлинности на **Azure Active Directory**.
    - Выберите **Single sign-on** (Единый вход). В качестве метода единого входа выберите Встроенная проверка подлинности Windows.
    - Задайте для **внутреннего субъекта-службы приложения** имя субъекта-службы компьютера сервера печати.
    - Задайте для **делегированного удостоверения** пользователя имя участника.
    - Повторите процедуру для приложения Ентперисеклаудпринт.
    ![IWA единого входа AAD](../media/hybrid-cloud-print/AAD-SingleSignOn-IWA.png)

### <a name="step-6---configure-the-required-mdm-policies"></a>Шаг 6. Настройка необходимых политик MDM

1. Войдите в поставщик MDM.
2. Найдите группу политика печати корпоративного облака и настройте политики, следуя приведенным ниже рекомендациям.
    - Клаудпринтоаусаусорити = `https://login.microsoftonline.com/<Azure AD Directory ID>` . Идентификатор каталога можно найти в разделе Azure Active Directory свойства >.
    - Клаудпринтоаусклиентид = \( \) значение идентификатора клиента приложения для собственного приложения. Его можно найти в разделе Azure Active Directory > Регистрация приложений > выберите Общие сведения о > в собственном приложении.
    - Клаудпринтердисковерендпоинт = внешний URL-адрес приложения службы обнаружения Mopria. Его можно найти в разделе Azure Active Directory > корпоративные приложения > выберите прокси приложения службы обнаружения Mopria >. **Он должен быть точно таким же, но без замыкающего/**.
    - Моприадисковериресаурцеид = URI идентификатора приложения для приложения службы обнаружения Mopria. Его можно найти в разделе Azure Active Directory > Регистрация приложений > выберите приложение службы обнаружения Mopria > обзор. **Он должен быть точно таким же, как и в конце/**.
    - Клаудпринтресаурцеид = URI идентификатора приложения для приложения для печати в облаке предприятия. Его можно найти в разделе Azure Active Directory > Регистрация приложений > выберите Общие сведения о корпоративном облачном приложении для печати >. **Он должен быть точно таким же, как и в конце/**.
    - Дисковеримакспринтерлимит = \<a positive integer\> .

> [!NOTE]
> Если вы используете службу Microsoft Intune, эти параметры можно найти в категории "Облачный принтер".

|Отображаемое имя Intune                     |Политика                         |
|----------------------------------------|-------------------------------|
|URL-адрес обнаружения принтера                   |клаудпринтердисковерендпоинт  |
|URL-адрес центра доступа к принтерам            |клаудпринтоаусаусорити       |
|GUID собственного клиентского приложения Azure            |клаудпринтоаусклиентид        |
|URI ресурса службы печати              |клаудпринтресаурцеид           |
|Максимальное число принтеров для запроса (только для мобильных устройств)  |дисковеримакспринтерлимит       |
|URI ресурса службы обнаружения принтеров  |моприадисковериресаурцеид      |

> [!NOTE]
> Если группа политик печати в облаке недоступна, но поставщик MDM поддерживает параметры OMA-URI, можно задать те же политики.  Дополнительные сведения см. на [этой](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint#enterprisecloudprint-cloudprintoauthauthority) вкладке.

- Значения для OMA-URI
  - Клаудпринтоаусаусорити =./вендор/мсфт/Полици/конфиг/ентерприсеклаудпринт/клаудпринтоаусаусорити
    - Значение =`https://login.microsoftonline.com/<Azure AD Directory ID>`
  - Клаудпринтоаусклиентид =./вендор/мсфт/Полици/конфиг/ентерприсеклаудпринт/клаудпринтоаусклиентид
    - Значение =`<Azure AD Native App's Application ID>`
  - Клаудпринтердисковерендпоинт =./вендор/мсфт/Полици/конфиг/ентерприсеклаудпринт/клаудпринтердисковерендпоинт
    - Значение = внешний URL-адрес приложения службы обнаружения Mopria (должен быть точно таким же, но без конечной части `/` )
  - Моприадисковериресаурцеид =./вендор/мсфт/Полици/конфиг/ентерприсеклаудпринт/моприадисковериресаурцеид
    - Значение = URI идентификатора приложения для приложения службы обнаружения Mopria.
  - Клаудпринтресаурцеид =./вендор/мсфт/Полици/конфиг/ентерприсеклаудпринт/клаудпринтресаурцеид
    - Значение = URI идентификатора приложения для приложения для печати в облаке предприятия
  - Дисковеримакспринтерлимит =./вендор/мсфт/Полици/конфиг/ентерприсеклаудпринт/дисковеримакспринтерлимит
    - Value = положительное целое число

### <a name="step-7---publish-the-shared-printer"></a>Шаг 7. публикация общего принтера

1. Установите нужный принтер на сервере печати.
2. Предоставьте общий доступ к принтеру через пользовательский интерфейс свойств принтера.
3. Выберите требуемый набор пользователей для предоставления доступа.
4. Сохраните изменения и закройте окно Свойства принтера.
5. Подготовьте обновление Windows 10 для создателя или более поздней версии. Присоедините компьютер к Azure AD и войдите в систему как пользователь, который синхронизируется с локальной Active Directory и ему было предоставлено соответствующее разрешение на доступ к файлу Моприадевицедб. DB.
6. На компьютере с Windows 10 откройте командную строку Windows PowerShell с повышенными привилегиями.
    - Выполните указанные ниже команды.
        - `find-module -Name PublishCloudPrinter`чтобы убедиться, что компьютер может достичь коллекция PowerShell (PSGallery)
        - `install-module -Name PublishCloudPrinter`

            > Примечание. Вы можете увидеть обмен сообщениями о том, что "PSGallery" является недоверенным репозиторием.  Введите "y", чтобы продолжить установку.

        - `Publish-CloudPrinter`
        - Printer = имя общего принтера. Это имя должно точно совпадать с именем общего ресурса, отображаемым на вкладке " **общий доступ** " свойств принтера, которое открывается на сервере печати.

        ![Свойства принтера сервера печати](../media/hybrid-cloud-print/PrintServer-PrinterProperties.png)

        - Manufacturer = изготовитель принтера.
        - Model = модель принтера.
        - Орглокатион = строка JSON, указывающая расположение принтера, например

            `{attrs: [{category:country, vs:USA, depth:0}, {category:organization, vs:Microsoft, depth:1}, {category:site, vs:Redmond, WA, depth:2}, {category:building, vs:Building 1, depth:3}, {category:floor_number, vs:1, depth:4}, {category:room_name, vs:1111, depth:5}]}`

        - SDDL = строка SDDL, представляющая разрешения для принтера.
            - Войдите на сервер печати с правами администратора, а затем выполните следующую команду PowerShell для принтера, который нужно опубликовать: `(Get-Printer PrinterName -full).PermissionSDDL` .
            - Добавьте в результат из приведенной выше команды префикс **о:ба** AS. Пример: Если строка, возвращенная предыдущей командой, является Г:ДУД: (A; ОИЦИ; FA;;; WD), SDDL = О:баг: ДУД: (A; ОИЦИ; FA;;; WD).
        - Дисковерендпоинт = Войдите в портал Azure и получите строку из корпоративных приложений > приложение службы обнаружения Mopria > прокси приложения > внешний URL-адрес. Опустить конец/.
        - Принтсерверендпоинт = Войдите в портал Azure, а затем получите строку из корпоративных приложений > корпоративное приложение для печати в облаке > > внешний URL-адрес. Опустить конец/.
        - Азуреклиентид = идентификатор приложения зарегистрированного собственного приложения.
        - Азуретенантгуид = идентификатор каталога вашего клиента Azure AD.
        - Дисковериресаурцеид = URI идентификатора приложения для приложения службы обнаружения Mopria.

    - Также можно ввести все необходимые значения параметров в командной строке. Синтаксис выглядит следующим образом.

        `Publish-CloudPrinter -Printer <string> -Manufacturer <string> -Model <string> -OrgLocation <string> -Sddl <string> -DiscoveryEndpoint <string> -PrintServerEndpoint <string> -AzureClientId <string> -AzureTenantGuid <string> -DiscoveryResourceId <string>`

        Пример команды:

        `Publish-CloudPrinter -Printer HcpTestPrinter -Manufacturer Manufacturer1 -Model Model1 -OrgLocation '{attrs: [{category:country, vs:USA, depth:0}, {category:organization, vs:MyCompany, depth:1}, {category:site, vs:MyCity, State, depth:2}, {category:building, vs:Building 1, depth:3}, {category:floor_name, vs:1, depth:4}, {category:room_name, vs:1111, depth:5}]}' -Sddl O:BAG:DUD:(A;OICI;FA;;;WD) -DiscoveryEndpoint https://mopriadiscoveryservice-contoso.msappproxy.net/mcs -PrintServerEndpoint https://enterprisecloudprint-contoso.msappproxy.net/ecp -AzureClientId dbe4feeb-cb69-40fc-91aa-73272f6d8fe1 -AzureTenantGuid 8de6a14a-5a23-4c1c-9ae4-1481ce356034 -DiscoveryResourceId https://mopriadiscoveryservice-contoso.msappproxy.net/mcs/`

    - Используйте следующую команду, чтобы убедиться, что принтер опубликован.

        `Publish-CloudPrinter -Query -DiscoveryEndpoint <string> -AzureClientId <string> -AzureTenantGuid <string> -DiscoveryResourceId <string>`

        Пример команды:

        `Publish-CloudPrinter -Query -DiscoveryEndpoint https://mopriadiscoveryservice-contoso.msappproxy.net/mcs -AzureClientId dbe4feeb-cb69-40fc-91aa-73272f6d8fe1 -AzureTenantGuid 8de6a14a-5a23-4c1c-9ae4-1481ce356034 -DiscoveryResourceId https://mopriadiscoveryservice-contoso.msappproxy.net/mcs/`

## <a name="verify-the-deployment"></a>Проверка развертывания

На устройстве, присоединенном к Azure AD, для которого настроены политики MDM:
- Откройте веб-браузер и перейдите к https://mopriadiscoveryservice- *имени клиента*. msappproxy.NET/MCS/Services.
- Вы должны увидеть текст JSON, описывающий набор функциональных возможностей этой конечной точки.
- Последовательно выберите **Параметры**  >  **устройства**  >  **принтеры & сканеры**.
    - Щелкните **Добавить принтер или сканер**.
    - Вы увидите ссылку на поиск по облачным принтерам (или по ссылке Поиск принтеров в моей организации на более новой машине Windows 10).
    - Щелкните ссылку.
    - Щелкните ссылку "выберите расположение для поиска".
        - Вы должны увидеть иерархию расположения устройства.
    - Выберите расположение и нажмите кнопку " **ОК** ", а затем кнопку " **Поиск** ", чтобы найти принтеры.
    - Выберите принтер и нажмите кнопку **Добавить устройство** .
    - После успешной установки принтера распечатайте его на принтере из избранного приложения.

> Примечание. Если используется принтер Екппринттест, выходной файл можно найти на компьютере сервера печати в папке C: \\ екптестаутпут \\ екптестпринт. XPS.

## <a name="troubleshooting"></a>Устранение неполадок

Ниже приведены распространенные проблемы при развертывании HCP.

|Ошибка |Рекомендуемые действия |
|------|------|
|Сбой сценария PowerShell Клаудпринтдеплой | <ul><li>Убедитесь, что Windows Server имеет Последнее обновление.</li><li>Если используется Windows Server Update Services (WSUS), см. статью [как создавать компоненты по запросу и языковые пакеты, доступные при использовании WSUS или SCCM](https://docs.microsoft.com/windows/deployment/update/fod-and-lang-packs).</li></ul> |
|Сбой установки SQLite с сообщением: обнаружен цикл зависимостей для пакета "System. Data. SQLite" | Install-Package System. Data. SQLite. Core-ProviderName NuGet-СкипдепенденЦиес<br>Install-Package System. Data. SQLite. EF6-ProviderName NuGet-СкипдепенденЦиес<br>Install-Package System. Data. SQLite. LINQ-ProviderName NuGet-СкипдепенденЦиес<br><br>После успешной загрузки пакетов убедитесь, что они имеют одинаковую версию. В противном случае добавьте параметр-requiredversion в приведенные выше команды и присвойте им одинаковую версию. |
|Не удалось опубликовать принтер | <ul><li>Для сквозной предварительной проверки подлинности убедитесь, что пользователю, публикующий принтер, предоставлено правильное разрешение для базы данных публикации.</li><li>Для предварительной проверки подлинности Azure AD убедитесь, что в службах IIS включена проверка подлинности Windows. См. шаг 5,3. Кроме того, сначала попробуйте пройти предварительную проверку подлинности. Если транзитная Предварительная проверка подлинности работает, скорее всего, эта ошибка связана с прокси приложения. См. статью [Устранение неполадок прокси-сервера приложений и сообщений об ошибках](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-troubleshoot). Обратите внимание, что переключение на сквозной сброс параметров единого входа. Перейдите к шагу 5, чтобы снова настроить предварительную проверку подлинности Azure AD.</li></ul> |
|Задания печати остаются в состоянии "Отправлено" в состояние принтера | <ul><li>Убедитесь, что TLS 1,2 включен на сервере соединителя. См. связанную статью в шаге 2,1.</li><li>Убедитесь, что HTTP2 отключен на сервере соединителя. См. связанную статью в шаге 2,1.</li></ul> |

Ниже приведены расположения журналов, которые могут помочь в устранении неполадок.

|Компонент |Расположение журнала |
|------|------|
|Клиент Windows 10 | <ul><li>Чтобы просмотреть журнал операций Azure AD, используйте Просмотр событий. Щелкните **Start (запуск** ) и введите Просмотр событий. Перейдите к журналам приложений и служб > Microsoft > Windows > работы с AAD >.</li><li>Используйте центр обратной связи для сбора журналов. См. статью [Отправка отзывов в корпорацию Майкрософт с помощью приложения центра отзывов](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) .</li></ul> |
|Сервер соединителя | Чтобы просмотреть журнал прокси приложения, используйте Просмотр событий. Щелкните **Start (запуск** ) и введите Просмотр событий. Перейдите к журналам приложений и служб > Microsoft > AadApplicationProxy > Connector > администратор. |
|Сервер печати | Журналы для приложения службы обнаружения Mopria и приложения для печати в облаке предприятия можно найти по адресу C:\inetpub\logs\LogFiles\W3SVC1. |
