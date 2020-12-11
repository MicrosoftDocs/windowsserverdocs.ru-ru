---
description: 'Дополнительные сведения: создание веб-приложения с помощью OpenID Connect Connect с AD FS 2016 и более поздних версий'
ms.assetid: d282bb4e-38a0-4c7c-83d8-f6ea89278057
title: Создание веб-приложения с помощью OpenID Connect Connect с AD FS 2016 и более поздних версий
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.openlocfilehash: 24c6918cc4f0a438bd45317364207b71a5e9b192
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97041582"
---
# <a name="build-a-web-application-using-openid-connect-with-ad-fs-2016-and-later"></a>Создание веб-приложения с помощью OpenID Connect Connect с AD FS 2016 и более поздних версий

## <a name="pre-requisites"></a>Предварительные требования
Ниже приведен список предварительных требований, которые необходимы перед завершением этого документа. В этом документе предполагается, что AD FS установлен и создана AD FS ферма.

-   Клиентские средства GitHub

-   AD FS в Windows Server 2016 TP4; или более поздней версии

-   Visual Studio 2013 или более поздняя версия.

## <a name="create-an-application-group-in-ad-fs-2016-and-later"></a>Создание группы приложений в AD FS 2016 и более поздних версиях
В следующем разделе описано, как настроить группу приложений в AD FS 2016 и более поздних версий.

#### <a name="create-application-group"></a>Создание группы приложений

1.  В AD FS управления щелкните правой кнопкой мыши группы приложений и выберите команду **Добавить группу приложений**.

2.  В мастере группы приложений в поле Имя введите **адфсссо** и в разделе **клиент-серверные приложения** выберите **веб-браузер, обращающийся к шаблону веб-приложения** .  Нажмите кнопку **Далее**.

    ![AD FS OpenID Connect](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_1.PNG)

3.  Скопируйте значение **идентификатора клиента** .  Он будет использоваться позже в качестве значения для Ida: ClientId в файле web.config приложений.

4.  Введите следующую команду для **URI перенаправления:**  -  **https://localhost:44320/** .  Нажмите кнопку **Добавить**. Нажмите кнопку **Далее**.

    ![AD FS OpenID Connect](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_2.PNG)

5.  На экране **Сводка** нажмите кнопку **Далее**.

    ![AD FS OpenID Connect](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_3.PNG)

6.  На экране **Завершение** нажмите кнопку **Закрыть**.

## <a name="download-and-modify-sample-application-to-authenticate-via-openid-connect-and-ad-fs"></a>Скачайте и измените пример приложения для проверки подлинности с помощью OpenID Connect Connect и AD FS
В этом разделе описывается, как скачать пример веб-приложения и изменить его в Visual Studio.   Мы будем использовать пример Azure AD, приведенный [здесь](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect).

Чтобы скачать пример проекта, используйте Git Bash и введите следующую команду:

```
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect
```

![AD FS OpenID Connect](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_8.PNG)

#### <a name="to-modify-the-app"></a>Изменение приложения

1.  Откройте пример с помощью Visual Studio.

2.  Перестройте приложение, чтобы восстановить все отсутствующие NuGet.

3.  Откройте файл web.config.  Измените следующие значения, чтобы они выглядели следующим образом:

    ```
    <add key="ida:ClientId" value="[Replace this Client Id from #3 in above section]" />
    <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->
    <add key="ida:PostLogoutRedirectUri" value="[Replace this with Redirect URI from #4 in the above section]" />
    ```

    ![AD FS OpenID Connect](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_9.PNG)

4.  Откройте файл Startup.Auth.cs и внесите следующие изменения:

    -   Закомментируйте следующее:

        ```
        //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);
        ```

    -   Настройте логику инициализации по промежуточного слоя OpenID Connect Connect со следующими изменениями:

        ```
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];
        ```

        ![AD FS OpenID Connect](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_10.PNG)

    -   Далее измените параметры по промежуточного слоя OpenID Connect Connect следующим образом:

        ```
        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                ClientId = clientId,
                //Authority = authority,
                MetadataAddress = metadataAddress,
                PostLogoutRedirectUri = postLogoutRedirectUri,
                RedirectUri = postLogoutRedirectUri
        ```

        ![AD FS OpenID Connect](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_11.PNG)

        Изменяя описанный выше способ, мы делаем следующее:

        -   Вместо использования центра для передачи данных о доверенном издателе мы указываем расположение документа обнаружения непосредственно через MetadataAddress

        -   Azure AD не обеспечивает принудительное присутствие redirect_uri в запросе, но ADFS делает это. Поэтому нам нужно добавить его здесь

## <a name="verify-the-app-is-working"></a>Проверка работоспособности приложения
После внесения приведенных выше изменений нажмите клавишу F5.  Откроется пример страницы.  Щелкните Вход.

![AD FS OpenID Connect](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_12.PNG)

Вы будете перенаправлены на страницу входа AD FS.  Выполните вход.

![AD FS OpenID Connect](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_13.PNG)

После успешного выполнения этой операции вы увидите, что вы вошли в.

![AD FS OpenID Connect](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_14.PNG)

## <a name="next-steps"></a>Next Steps
[Разработка AD FS](../../ad-fs/AD-FS-Development.md)
