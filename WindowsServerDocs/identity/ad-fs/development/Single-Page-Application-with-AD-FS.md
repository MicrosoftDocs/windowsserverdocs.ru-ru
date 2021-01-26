---
title: Создание веб-приложения с одной страницей с помощью OAuth и ADAL.JS с AD FS 2016 или более поздней версии
description: Пошаговое руководство, содержащее инструкции по проверке подлинности в AD FS с помощью ADAL для JavaScript защита одностраничного приложения на базе AngularJS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/13/2018
ms.topic: article
ms.openlocfilehash: 7e3299d9d33690066206a5698958f95663414ae4
ms.sourcegitcommit: 6717decb5839aa340c81811d6fde020aabaddb3b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98781812"
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016-or-later"></a>Создание веб-приложения с одной страницей с помощью OAuth и ADAL.JS с AD FS 2016 или более поздней версии

В этом пошаговом руководстве приведена инструкция по проверке подлинности в AD FS с помощью ADAL для JavaScript защита одностраничного приложения на базе AngularJS, реализованного с помощью веб-API ASP.NET серверной части.

В этом сценарии при входе пользователя в систему интерфейсная часть JavaScript использует [библиотеку проверки подлинности Active Directory для JavaScript (ADAL.JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js) и неявное предоставление авторизации для получения маркера идентификатора (id_token) из Azure AD. Маркер кэшируется, а клиент присоединяет его к запросу как маркер носителя при отправке вызовов в свою серверную часть веб-API, для защиты которого применяется ПО промежуточного слоя OWIN.

> [!IMPORTANT]
> Пример, который можно создать здесь, предназначен только для образовательных целей. Эти инструкции предназначены для самой простой и минимальной реализации, которая может предоставить необходимые элементы модели. Пример может не включать все аспекты обработки ошибок и другие функции связывания.

> [!NOTE]
> Это пошаговое руководство применимо **только** к AD FS Server 2016 и более поздних версий

## <a name="overview"></a>Обзор
В этом примере мы создадим поток проверки подлинности, где клиент одностраничного приложения будет проходить проверку подлинности в AD FS для безопасного доступа к ресурсам WebAPI в серверной части. Ниже приведен общий поток проверки подлинности

![Авторизация AD FS](media/Single-Page-Application-with-AD-FS/authenticationflow.png)

При использовании одностраничного приложения пользователь переходит в начальное расположение, откуда загружаются Начальная страница и коллекция файлов JavaScript и HTML-представления. Необходимо настроить Библиотека проверки подлинности Active Directory (ADAL), чтобы узнать важную информацию о приложении, т. е. экземпляр AD FS, идентификатор клиента, чтобы он мог направить проверку подлинности в AD FS.

Если ADAL видит триггер для проверки подлинности, он использует сведения, предоставленные приложением, и направляет проверку подлинности AD FS STS.  Одностраничное приложение, зарегистрированное как общедоступный клиент в AD FS, автоматически настраивается на неявный поток предоставления. Запрос авторизации приводит к возвращению маркера идентификации, возвращаемого приложению через #fragment. Последующие вызовы серверной части WebAPI будут содержать этот маркер идентификации в качестве токена носителя в заголовке для получения доступа к WebAPI.

## <a name="setting-up-the-development-box"></a>Настройка поля разработки
В этом пошаговом руководстве используется Visual Studio 2015. В проекте используется библиотека ADAL JS. Дополнительные сведения о ADAL см. в статье [Библиотека проверки подлинности Active Directory .NET.](/dotnet/api/microsoft.identitymodel.clients.activedirectory)

## <a name="setting-up-the-environment"></a>Настройка среды
В этом пошаговом руководстве мы будем использовать базовую установку:

1. DC: контроллер домена для домена, в котором будет размещаться AD FS
2. AD FS Server — сервер AD FS для домена.
3. Компьютер для разработки: компьютер, на котором установлена Visual Studio и который будет разрабатывать наш пример

При необходимости можно использовать только два компьютера. Один для DC/AD FS, а другой — для разработки образца.

Настройка контроллера домена и AD FS выходит за рамки этой статьи. Дополнительные сведения о развертывании см. в следующих статьях:

- [Развертывание доменных служб Active Directory](../../ad-ds/deploy/AD-DS-Deployment.md)
- [Развертывание AD FS](../AD-FS-Deployment.md)

## <a name="clone-or-download-this-repository"></a>Клонирование или скачивание этого репозитория
Мы будем использовать пример приложения, созданного для интеграции Azure AD, в одностраничное приложение AngularJS и изменив его, чтобы защитить серверный ресурс с помощью AD FS.

Из оболочки или командной строки:

```
git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git
```

## <a name="about-the-code"></a>О коде
Ниже приведены основные файлы, содержащие логику проверки подлинности.

**App.js** — внедряет зависимость модуля ADAL, предоставляет значения конфигурации приложения, используемые ADAL для взаимодействия протокола с AAD, и указывает, какие маршруты не должны быть доступны без предыдущей проверки подлинности.

**index.html** — содержит ссылку на adal.js

**HomeController.js**— показывает, как использовать преимущества методов Login () и logOut () в ADAL.

**UserDataController.js** — показано, как извлечь сведения о пользователе из кэшированной id_token.

**Startup.auth.CS** — содержит конфигурацию WebAPI для использования Active Directory служба федерации для проверки подлинности носителя.

## <a name="registering-the-public-client-in-ad-fs"></a>Регистрация общедоступного клиента в AD FS
В примере WebAPI настроен для прослушивания в https://localhost:44326/ . **Веб-браузер группы приложений, обращающийся к веб-приложению,** можно использовать для настройки неявного приложения потока предоставления.

1. Откройте консоль управления AD FS и щелкните **Добавить группу приложений**. В **мастере добавления группы приложений** введите имя приложения, описание и выберите **веб-браузер, обращающийся к** шаблону веб-приложения из раздела **клиент-сервер приложения** , как показано ниже.

    ![Снимок экрана: страница приветствия мастера добавления группы приложений, показывающая веб-браузер, обращающийся к выбранному шаблону веб-приложения.](media/Single-Page-Application-with-AD-FS/appgroup_step1.png)

2. На следующей странице **собственное приложение** укажите идентификатор клиента приложения и URI перенаправления, как показано ниже.

    ![Снимок экрана: страница "собственное приложение" мастера добавления группы приложений, отображающая перенаправление U R I.](media/Single-Page-Application-with-AD-FS/appgroup_step2.png)

3. На следующей странице **Примените политику контроля доступа** , чтобы оставить разрешения для *всех*

4. Страница сводки должна выглядеть примерно так, как показано ниже.

    ![Снимок экрана со страницей "Сводка" мастера добавления группы приложений.](media/Single-Page-Application-with-AD-FS/appgroup_step3.png)

5. Нажмите кнопку **Далее** , чтобы завершить добавление группы приложений и закрыть мастер.

## <a name="modifying-the-sample"></a>Изменение образца
Настройка ADAL JS

Откройте файл **app.js** и измените определение **adalProvider.init** на:

```
    adalProvider.init(
        {
            instance: 'https://fs.contoso.com/',                // your STS URL
            tenant: 'adfs',                                     // this should be set to adfs
            clientId: '150ab73e-0b05-4b78-9e50-0095a992cca9',   // set this to the Client Id generated during application registration in AD FS
            popUp: false,
            //cacheLocation: 'localStorage',                    // enable this for IE, as sessionStorage does not work for localhost.
        },
        $httpProvider
    );
```

| Конфигурация | Описание |
| ------------- | ----------- |
| экземпляр | URL-адрес STS, например https://fs.contoso.com/ |
| tenant | Не заключайте его в "ADFS" |
| clientID | Это идентификатор клиента, указанный при настройке общедоступного клиента для приложения с одной страницей |

## <a name="configure-webapi-to-use-ad-fs"></a>Настройка WebAPI для использования AD FS
Откройте файл **Startup.auth.CS** в образце и добавьте в начало следующую команду:

```
    using System.IdentityModel.Tokens;

remove:

    app.UseWindowsAzureActiveDirectoryBearerAuthentication(
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions
        {
            Audience = ConfigurationManager.AppSettings["ida:Audience"],
            Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
        }
    );

and add:

    app.UseActiveDirectoryFederationServicesBearerAuthentication(
        new ActiveDirectoryFederationServicesBearerAuthenticationOptions
        {
            MetadataEndpoint = ConfigurationManager.AppSettings["ida:AdfsMetadataEndpoint"],
            TokenValidationParameters = new TokenValidationParameters()
            {
                ValidAudience = ConfigurationManager.AppSettings["ida:Audience"],
                ValidIssuer = ConfigurationManager.AppSettings["ida:Issuer"]
            }
        }
    );
```

| Параметр | Описание |
| --------- | ----------- |
| валидаудиенце | При этом настраивается значение "аудитория", которое будет проверяться в токене. |
| валидиссуер | При этом настраивается значение Issuer, для которого будет выполнена проверка в токене |
| MetadataEndpoint | Это указывает на сведения о метаданных STS |

## <a name="add-application-configuration-for-ad-fs"></a>Добавление конфигурации приложения для AD FS
Измените XML-файл appSettings, как показано ниже:

```xml
<appSettings>
    <add key="ida:Audience" value="https://localhost:44326/" />
    <add key="ida:AdfsMetadataEndpoint" value="https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml" />
    <add key="ida:Issuer" value="https://fs.contoso.com/adfs" />
</appSettings>
```

## <a name="running-the-solution"></a>Запуск решения
Очистите решение, перестройте решение и запустите его. Если вы хотите просмотреть подробные трассировки, запустите Fiddler и включите расшифровку HTTPS.

В браузере (используйте браузер Chrome) будет загружено SPA, а появится следующий экран:

![Регистрация клиента](media/Single-Page-Application-with-AD-FS/singleapp3.png)

Щелкните имя входа.  Список ToDo будет активировать поток проверки подлинности, а ADAL JS будет направлять проверку подлинности на AD FS

![Вход](media/Single-Page-Application-with-AD-FS/singleapp4a.png)

В Fiddler можно увидеть маркер, возвращаемый как часть URL-адреса в фрагменте #.

![Снимок экрана Fiddler показывает, что маркер, возвращаемый в качестве части URL-адреса, можно увидеть в фрагменте # Fragment.](media/Single-Page-Application-with-AD-FS/singleapp5a.png)

Теперь вы можете вызвать API серверной части, чтобы добавить элементы списка ToDo для вошедшего в систему пользователя:

![Снимок экрана примера приложения ADAL JS.](media/Single-Page-Application-with-AD-FS/singleapp6.png)

## <a name="next-steps"></a>Next Steps
[Разработка AD FS](../../ad-fs/AD-FS-Development.md)
