---
description: Дополнительные сведения о создании приложения на стороне сервера с использованием конфиденциальных клиентов OAuth с AD FS 2016 или более поздней версии.
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: Создание приложения на стороне сервера с использованием конфиденциальных клиентов OAuth с AD FS 2016 или более поздней версии
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.openlocfilehash: 5c256d63bf08d6e9c3aa91e5aa7099822c507b81
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97046462"
---
# <a name="build-a-server-side-application-using-oauth-confidential-clients-with-ad-fs-2016-or-later"></a>Создание приложения на стороне сервера с использованием конфиденциальных клиентов OAuth с AD FS 2016 или более поздней версии


AD FS 2016 и более поздних выпусков обеспечивают поддержку клиентов, способных поддерживать собственный секрет, например приложение или службу, выполняемые на веб-сервере.  Эти клиенты называются конфиденциальными клиентами.
Ниже приведена схема веб-приложения, работающего на веб-сервере и обслуживающего конфиденциальный клиент для AD FS:

## <a name="pre-requisites"></a>Предварительные требования
Ниже приведен список предварительных требований, которые необходимы перед завершением этого документа. В этом документе предполагается, что AD FS установлен.

-   Клиентские средства GitHub

-   AD FS в Windows Server 2016 TP4; или более поздней версии

-   Visual Studio 2013 или более поздняя версия.

## <a name="create-an-application-group-in-ad-fs-2016-or-later"></a>Создание группы приложений в AD FS 2016 или более поздней версии
В следующем разделе описано, как настроить группу приложений в AD FS 2016 или более поздней версии.

#### <a name="create-the-application-group"></a>Создание группы приложений

1.  В AD FS управления щелкните правой кнопкой мыши группы приложений и выберите команду **Добавить группу приложений**.

2.  В мастере группы приложений в поле **имя** введите **адфсоаускк** и в разделе **клиент-сервер приложения** выберите **серверное приложение, осуществляющее доступ к шаблону веб-API** .  Нажмите кнопку **Далее**.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG)

3.  Скопируйте значение **идентификатора клиента** .  Он будет использоваться позже в качестве значения для **Ida: ClientID** в файле web.config приложений.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG)

4.  Введите следующую команду для **URI перенаправления:**  -  **https://localhost:44323** .  Нажмите кнопку **Добавить**. Нажмите кнопку **Далее**.

5.  На экране **Настройка учетных данных приложения** установите флажок **создать общий секрет** и скопируйте секретный код.  Он будет использоваться позже в качестве значения для **Ida: ClientSecret** в файле web.config приложений.  Нажмите кнопку **Далее**.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG)

6. На экране **Настройка веб-API** введите следующую команду в поле **идентификатор**  -  **https://contoso.com/WebApp** .  Нажмите кнопку **Добавить**. Нажмите кнопку **Далее**.  Это значение будет использоваться позже для **Ida: графресаурцеид** в файле web.config приложений.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG)

7. На экране **Применить политику управления доступом** выберите **разрешение все** и нажмите кнопку **Далее**.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG)

8. На экране **Настройка разрешений приложения** убедитесь, что **OpenID Connect** и **user_impersonation** выбраны, и нажмите кнопку **Далее**.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG)

9. На экране **Сводка** нажмите кнопку **Далее**.

10. На экране **Завершение** нажмите кнопку **Закрыть**.

## <a name="upgrade-the-database"></a>Обновление базы данных
Для создания этого пошагового руководства использовалась Visual Studio 2015.   Чтобы получить пример работы с Visual Studio 2015, необходимо обновить файл базы данных.  Выполните следующие действия.

В этом разделе описывается, как скачать пример веб-API и обновить базу данных в Visual Studio 2015.   Мы будем использовать пример Azure AD, приведенный [здесь](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity).

Чтобы скачать пример проекта, используйте Git Bash и введите следующую команду:

```
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git
```

![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)

#### <a name="to-upgrade-the-database-file"></a>Обновление файла базы данных

1.  Откройте проект в Visual Studio. появится всплывающее окно с сообщением о том, что приложению требуется SQL Server 2012 Express или необходимо обновить базу данных.  Нажмите кнопку "ОК".

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)

2.  Затем скомпилируйте приложение, выбрав Build-> Build Solution (в верхней части).  При этом будут восстановлены все пакеты NuGet.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)

3.  Теперь в верхней части страницы выберите **Просмотр**  ->  **Обозреватель сервера**.  После открытия в разделе **подключения к данным** щелкните правой кнопкой мыши **DefaultConnection** и выберите пункт **изменить подключение**.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)

4.  При **изменении соединения** в поле **имя файла базы данных (новое или существующее)** выберите **Обзор** и укажите **пас\филенаме.МДФ**. Нажмите кнопку **Да** в диалоговом окне.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)

5.  В меню **изменить подключение** выберите **Дополнительно**.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)

6.  В окне Дополнительные свойства выберите источник данных и с помощью раскрывающегося списка измените его с **(LocalDb\v11.0)** на **(LocalDb) \MSSQLLocalDB**.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)

7.  Нажмите кнопку "ОК". Нажмите кнопку "ОК".  Нажмите кнопку Да, чтобы обновить базу данных.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)

8.  Когда это завершится, скопируйте значение в поле, расположенное справа от **строки подключения.**

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)

9.  Теперь откройте файл Web.config и замените значение в connectionString на значение, скопированное ранее.  Сохраните файл Web.config.

    > [!NOTE]
    > Чтобы получить новый параметр connectionString, необходимо выполнить описанные выше действия.  В противном случае при выполнении Update-Database ниже произойдет ошибка.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)

10. В верхней части Visual Studio выберите **Просмотреть**  ->  **другие**  ->  **консоль диспетчера пакетов** Windows.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)

11. В нижней части консоли диспетчера пакетов введите:  `Enable-Migrations` и нажмите клавишу ВВОД.

    > [!NOTE]
    > Если появляется сообщение о том, что Enable-Migrations не распознан как командлет, введите Install-Package EntityFramework для обновления EntityFramework.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)

12. В нижней части консоли диспетчера пакетов введите:  `Add-Migration <anynamehere>` и нажмите клавишу ВВОД.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)

13. В нижней части консоли диспетчера пакетов введите:  `Update-Database` и нажмите клавишу ВВОД.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)

## <a name="modify-the-webapi-in-visual-studio"></a>Изменение WebApi в Visual Studio

#### <a name="to-modify-the-sample-web-api"></a>Изменение примера веб-API

1.  Откройте пример с помощью Visual Studio.

2.  Откройте файл web.config.  Измените следующие значения:

    -   IDA: ClientId — введите значение из #3 в разделе Создание группы приложений выше.

    -   IDA: ClientSecret — введите значение из #5 в разделе Создание группы приложений выше.

    -   IDA: Графресаурцеид — введите значение из #6 в разделе Создание группы приложений выше.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)

3.  Откройте файл Startup.Auth.cs в разделе App_Start и внесите следующие изменения:

    -   Закомментируйте следующие строки:

        ```
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);
        ```

    -   Добавьте в его место следующее:

        ```
        public static readonly string Authority = "https://<your_fsname>/adfs";
        ```

        где <your_fsname> заменяется частью DNS URL-адреса службы федерации, например adfs.contoso.com

        ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)

4.  Откройте файл UserProfileController.cs и внесите следующие изменения:

    -   Закомментируйте следующее:

        ```
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));
        ```

    -   Замените оба вхождения следующим:

        ```
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));
        ```

        ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)

    -   Закомментируйте следующее:

        ```
        //authContext = new AuthenticationContext(Startup.Authority);
        ```

    -   Замените оба вхождения следующим:

        ```
        authContext = new AuthenticationContext(Startup.Authority, false);
        ```

        ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)

    -   Теперь закомментируйте все экземпляры следующего:

        ```
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString() + "/OAuth");
        ```

    -   Замените все вхождения следующим:

        ```
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString());
        ```

        ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)

## <a name="test-the-solution"></a>Тестирование решения
В этом разделе будет протестировать конфиденциальное клиентское решение.  Для тестирования решения используйте следующую процедуру.

#### <a name="testing-the-confidential-client-solution"></a>Тестирование решения для конфиденциального клиента

1. В верхней части Visual Studio убедитесь, что выбран Internet Explorer, и щелкните зеленую стрелку.

   ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)

2. Получив страницу ASP.Net, щелкните **зарегистрировать** в верхней правой части страницы.  Введите имя пользователя и пароль, затем нажмите кнопку **зарегистрировать** .  В базе данных SQL будет создана локальная учетная запись.

   ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)

3. Обратите внимание, что веб-сайт ASP.NET говорит привет abby@contoso.com !.  Щелкните **Профиль**.

   ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG)

4. Это приводит к отображению страницы без каких-либо сведений и говорит о том, что для входа необходимо щелкнуть здесь.  Щелкните **здесь**.

   ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG)

5. Теперь вам будет предложено войти в AD FS.

   ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG)

## <a name="next-steps"></a>Next Steps
[Разработка AD FS](../../ad-fs/AD-FS-Development.md)
