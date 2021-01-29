---
description: Создайте приложение на стороне сервера, использующее конфиденциальные клиенты OAuth. Используйте AD FS 2016 или более поздней версии.
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: Создание приложения на стороне сервера, использующего конфиденциальные клиенты OAuth, с помощью службы федерации Active Directory (AD FS) 2016 или более поздней версии
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.openlocfilehash: 2302d8fd1d6d00943316a62578d1d8d9ee096169
ms.sourcegitcommit: d1815253b47e776fb96a3e91556fd231bef8ee6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2021
ms.locfileid: "99042580"
---
# <a name="build-a-server-side-app-that-uses-oauth-confidential-clients-by-using-ad-fs-2016-or-later"></a>Создание приложения на стороне сервера, использующего конфиденциальные клиенты OAuth, с помощью AD FS 2016 или более поздней версии


Службы федерации Active Directory (AD FS) (AD FS) 2016 и более поздних версий поддерживает клиенты, которые могут поддерживать собственный секрет, например приложение или службу, выполняемые на веб-сервере.  Эти клиенты называются *конфиденциальными клиентами*.

В этой статье описывается веб-приложение, выполняемое на веб-сервере. Приложение выступает в качестве конфиденциального клиента для AD FS.

## <a name="prerequisites"></a>Предварительные требования
Вам потребуются следующие ресурсы: 

-   Клиентские средства GitHub.

-   AD FS в Windows Server 2016 Technical Preview 4 или более поздней версии. (В этой статье предполагается, что AD FS установлен.)

-   Visual Studio 2013 или более поздняя версия.

## <a name="create-an-application-group"></a>Создание группы приложений

Чтобы создать группу приложений в AD FS 2016 или более поздней версии:

1.  В AD FS Управление щелкните правой кнопкой мыши **группы приложений**. Затем выберите **Добавить группу приложений**.

2.  В **мастере добавления группы приложений** выполните следующие действия. 
    1. В поле **имя** введите *адфсоаускк*. 
    1. В разделе **клиент-серверные приложения** выберите **серверное приложение, осуществляющее доступ к шаблону веб-API** .  
    1. Выберите **Далее**.

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG" alt-text="Снимок экрана, на котором показано, где выбрать шаблон для серверного приложения, которое обращается к веб-A P I." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG":::

3.  Скопируйте значение **идентификатора клиента** . Он будет использоваться позже в файле *web.config* приложения. Это значение для `ida:ClientId` .

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG" alt-text="Снимок экрана, на котором показано, куда копировать значение идентификатора клиента." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG":::

4. В качестве **URI перенаправления** введите *https://localhost:44323* .  Выберите **Добавить**, а затем нажмите кнопку **Далее**.

5.  На странице **Настройка учетных данных приложения** выполните следующие действия. 
    1. Выберите **создать общий секрет**. 
    1. Скопируйте секрет. Этот секрет будет использоваться позже в файле *web.config* приложения. Это значение для `ida:ClientSecret` .  
    1. Выберите **Далее**.

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG" alt-text="Снимок экрана, на котором показана страница настройки учетных данных приложения." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG":::

6. На странице **Настройка веб-API** выполните следующие действия. 
    1. В качестве **идентификатора** введите *https://contoso.com/WebApp* . Это значение будет использоваться позже в файле *web.config* приложения. Это значение для `ida:GraphResourceId` . 
    1. Выберите **Добавить**. 
    1. Выберите **Далее**.  

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG" alt-text="Снимок экрана, на котором показана страница Настройка Web A P I." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG":::

7. На странице **применение политики контроля доступа** выберите **разрешение все**. Нажмите кнопку **Далее**.

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG" alt-text="Снимок экрана, на котором показана страница &quot;применение политики контроля доступа&quot;." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG":::

8. На странице **Настройка разрешений приложения** убедитесь, что выбраны **OpenID Connect** и **user_impersonation** . Нажмите кнопку **Далее**.

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG" alt-text="Снимок экрана, на котором показана страница &quot;Настройка разрешений приложения&quot;." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG":::

9. На странице **Сводка** нажмите кнопку **Далее**.

10. На странице **Завершение** нажмите кнопку **Закрыть**.

## <a name="upgrade-the-database"></a>Обновление базы данных
Эта статья основана на Visual Studio 2015. Чтобы сделать пример работать с Visual Studio 2015, обновите файл базы данных, следуя инструкциям в этом разделе.

В этом разделе описывается, как скачать пример веб-API и обновить базу данных в Visual Studio 2015. Мы используем [пример Azure Active Directory](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity).

Чтобы скачать пример проекта, в Git Bash введите следующую команду:

```
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git
```

![Снимок экрана, показывающий, как скачать пример проекта.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)

Чтобы обновить файл базы данных, выполните следующие действия.

1.  Откройте проект в Visual Studio. В появившемся окне появится сообщение о том, что приложению требуется SQL Server 2012 Express. Если у вас нет SQL Server 2012 Express, необходимо обновить базу данных.  Щелкните **ОК**.

    ![Снимок экрана, на котором показано сообщение о том, что для приложения требуется сервер Q L Server 2012 Express. В противном случае необходимо обновить базу данных.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)

2. В верхней части окна скомпилируйте приложение, выбрав **Сборка** сборка  >  **решения**. Будут восстановлены все пакеты NuGet.

    ![Снимок экрана, на котором показано, что восстановление пакетов NuGet прошло успешно.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)

3.  В верхней части окна выберите **Просмотреть**  >  **Обозреватель сервера**.  В открывшейся области в разделе **подключения к данным** щелкните правой кнопкой мыши **DefaultConnection** и выберите пункт **изменить подключение**.

    ![Снимок экрана, посвященный элементу меню "изменить подключение".](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)

4.  В окне **изменение соединения** в разделе **имя файла базы данных (новое или существующее)** нажмите кнопку **Обзор**. Введите *пас\филенаме.МДФ*. Затем в диалоговом окне выберите **Да**.

    ![Снимок экрана, показывающий диалоговое окно для создания файла базы данных.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)

5.  В диалоговом окне **изменение соединения** выберите **Дополнительно**.

    ![Снимок экрана, на котором показана кнопка "Дополнительно".](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)

6.  В диалоговом окне **Дополнительные свойства** в разделе **источник данных** измените **(LocalDb\v11.0)** на **\MSSQLLocalDB (LocalDb)**.

    ![Снимок экрана, на котором выделено поле источника данных.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)

7.  Щелкните **ОК** > **ОК**. Затем нажмите кнопку **Да** , чтобы обновить базу данных.

    ![Снимок экрана, на котором показано диалоговое окно обновления базы данных.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)

8.  После завершения процесса в правой части скопируйте значение в поле **строка подключения** .

    ![Снимок экрана, на котором показано поле строки подключения.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)

9.  Откройте файл *web.config* и замените `connectionString` значение значением, скопированным ранее.  Сохраните файл *web.config* .

    > [!NOTE]
    > Чтобы получить новую строку подключения, необходимо выполнить описанные выше действия. В противном случае при выполнении этой статьи будут возникнет ошибка `Update-Database` .

    ![Снимок экрана, на котором показано, где найти значение строки подключения.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)

10. В верхней части окна Visual Studio выберите **Просмотреть**  >  **другие**  >  **консоль диспетчера пакетов** Windows.

    ![Снимок экрана, посвященный пункту меню консоли диспетчера пакетов.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)

11. В области **консоли диспетчера пакетов** введите  `Enable-Migrations` .

    > [!NOTE]
    > Если появится сообщение об ошибке "Enable-migrations не распознается как командлет", введите *Install-package entityframework* , чтобы обновить Entity Framework.

    ![Снимок экрана, на котором показано, куда войти, чтобы включить миграцию.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)

12. Введите `Add-Migration <AnyNameHere>`.

    ![Снимок экрана, на котором показано, куда войти Add-Migration тест.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)

13. Введите `Update-Database`.

    ![Снимок экрана, на котором показано, куда войти обновление базы данных.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)

## <a name="modify-the-web-api"></a>Изменение веб-API 

Чтобы изменить пример веб-API в Visual Studio, выполните следующие действия.

1.  В Visual Studio откройте пример.

2.  Откройте файл *web.config* .  Измените следующие параметры, используя значения, скопированные в процедуре [Create a Application Group](#create-an-application-group) :

    -   `ida:ClientId`: Введите идентификатор клиента.

    -   `ida:ClientSecret`: Введите секрет клиента.

    -   `ida:GraphResourceId`: Введите идентификатор ресурса графа.

    ![Снимок экрана, на котором показаны значения, которые необходимо изменить.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)

3. В разделе **App_Start** откройте файл *Startup.auth.CS* . Внесите следующие изменения:

    -   Закомментируйте следующие строки:

        ```
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);
        ```

    -   Вместо удаленных строк добавьте следующую строку:

        ```
        public static readonly string Authority = "https://<your_fsname>/adfs";
        ```

        Здесь замените на `<your_fsname>` часть DNS URL-адреса службы федерации. Например, введите *ADFS.contoso.com*.

        ![Снимок экрана, показывающий изменения в файле начальной проверки подлинности в точке C S.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)

4.  Откройте файл *UserProfileController.CS* . Внесите следующие изменения:

    -   Закомментируйте следующую строку:

        ```
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));
        ```

    -   Замените оба вхождения следующим кодом:

        ```
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));
        ```

        ![Снимок экрана, показывающий изменения в файле контроллера профилей пользователей с точкой C S.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)

    -   Закомментируйте следующую строку:

        ```
        //authContext = new AuthenticationContext(Startup.Authority);
        ```

    -   Замените оба вхождения следующим кодом:

        ```
        authContext = new AuthenticationContext(Startup.Authority, false);
        ```

        ![Снимок экрана, на котором показаны изменения, внесенные в значение authContext.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)

    -   Закомментируйте все экземпляры следующей строки:

        ```
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString() + "/OAuth");
        ```

    -   Замените все вхождения следующим кодом:

        ```
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString());
        ```

        ![Снимок экрана, посвященный U R I перенаправлению U R I.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)

## <a name="test-the-solution"></a>Тестирование решения

Чтобы протестировать конфиденциальное клиентское решение:

1. В верхней части окна Visual Studio убедитесь, что выбран **Internet Explorer** . Затем щелкните зеленую стрелку.

   ![Снимок экрана, посвященный кнопке Internet Explorer.](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)

2. На открывшейся странице **ASP.NET** : 
    1. В правом верхнем углу выберите **зарегистрировать**.  
    1. Введите имя пользователя и пароль. 
    1. Выберите **зарегистрировать** , чтобы создать локальную учетную запись в базе данных SQL.

   :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG" alt-text="Снимок экрана, на котором показано, где создать локальную учетную запись в базе данных Q." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG":::

3. Обратите внимание на сообщение **Hello abby \@ contoso.com!**.  Выберите **профиль**.

   :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG" alt-text="Снимок экрана, который выделяет профиль." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG":::

4. На новой странице появится сообщение с запросом на вход.  Выберите **здесь**.

    :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG" alt-text="Снимок экрана, на котором показана страница профиля пользователя." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG":::

    Вам будет предложено войти в AD FS.

   :::image type="content" source="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG" alt-text="Снимок экрана, на котором показана страница входа для D F S." lightbox="media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG":::     
        
## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о [разработке AD FS](../../ad-fs/AD-FS-Development.md).
