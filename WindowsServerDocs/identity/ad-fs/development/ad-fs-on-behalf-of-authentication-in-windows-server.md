---
ms.assetid: 5052f13c-ff35-471d-bff5-00b5dd24f8aa
title: Создание многоуровневого приложения с использованием от имени (OBO) с помощью OAuth с AD FS 2016 или более поздней версии
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.openlocfilehash: b080f45d36d26ed566eacc5ae1ad84d98dd45d48
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/08/2020
ms.locfileid: "96864763"
---
# <a name="build-a-multi-tiered-application-using-on-behalf-of-obo-using-oauth-with-ad-fs-2016-or-later"></a>Создание многоуровневого приложения с использованием от имени (OBO) с помощью OAuth с AD FS 2016 или более поздней версии

В этом пошаговом руководстве приведена инструкция по реализации проверки подлинности от имени пользователя (OBO) с помощью AD FS в Windows Server 2016 TP5 или более поздней версии. Дополнительные сведения о проверке подлинности OBO см. в статье [AD FS OpenID Connect Connect/OAuth Flows и сценарии приложений](../../ad-fs/overview/ad-fs-openid-connect-oauth-flows-scenarios.md) .

> [!WARNING]
> Пример, который можно создать здесь, предназначен только для образовательных целей. Эти инструкции предназначены для самой простой и минимальной реализации, которая может предоставить необходимые элементы модели. Этот пример может не включать все аспекты обработки ошибок и другие функции связи и посвящен только получению успешной проверки подлинности OBO.

## <a name="overview"></a>Обзор

В этом примере будет создан поток проверки подлинности, в котором клиент будет обращаться к веб-службе среднего уровня, а веб-служба будет действовать от имени клиента, прошедшего проверку подлинности, чтобы получить маркер доступа.

![AD FS схемы от имени](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO28.png)

Ниже приведен поток проверки подлинности, который будет достигнут в примере.
1. Клиент выполняет проверку подлинности AD FS конечной точке авторизации и запрашивает код авторизации.
2. Конечная точка авторизации возвращает клиенту код проверки подлинности
3. Клиент использует код проверки подлинности и представляет его конечной точке токена AD FS, чтобы запросить маркер доступа для веб-службы среднего уровня как WebAPI
4. AD FS возвращает маркер доступа к веб-службе среднего уровня. Для получения дополнительных функциональных возможностей службе среднего уровня требуется доступ к серверной WebAPI.
5. Клиент использует маркер доступа для использования службы среднего уровня.
6. Служба среднего уровня предоставляет маркер доступа к маркеру AD FS маркера доступа для внутреннего пользователя, прошедшего проверку подлинности WebAPI.
7. AD FS возвращает маркер доступа для серверной части WebAPI в службу среднего уровня актиинг в качестве клиента
8. Служба среднего уровня использует маркер доступа, предоставленный AD FS на шаге 7 для доступа к серверной части WebAPI в качестве клиента и выполнения необходимых функций.

## <a name="sample-structure"></a>Пример структуры

Пример будет состоять из трех модулей

Модуль | Описание:
-------|------------
тодоклиент | Собственный клиент, с которым взаимодействует пользователь
Файле todoservice | Веб-API среднего уровня, который выступает в качестве клиента для серверной части WebAPI
вебапиобо | Внутренний веб-API, используемый файле todoservice для выполнения операции требования, когда пользователь добавляет ToDoItem

## <a name="setting-up-the-development-box"></a>Настройка поля разработки

В этом пошаговом руководстве используется Visual Studio 2015. Проект сильно использует Библиотека проверки подлинности Active Directory (ADAL). Дополнительные сведения о ADAL см. в статье [Библиотека проверки подлинности Active Directory .NET](/dotnet/api/microsoft.identitymodel.clients.activedirectory)

В примере также используется SQL LocalDB v 11.0. Прежде чем приступать к работе с примером, установите SQL LocalDB.

## <a name="setting-up-the-environment"></a>Настройка среды
Мы будем работать с базовой настройкой:

1. **DC**: контроллер домена для домена, в котором будет размещаться AD FS
2. **AD FS Server**— сервер AD FS для домена.
3. **Компьютер для разработки**: компьютер, на котором установлена Visual Studio и который будет разрабатывать наш пример

При необходимости можно использовать только два компьютера. Один для DC/ADFS, а другой — для разработки образца.

Настройка контроллера домена и AD FS выходит за рамки этой статьи. Дополнительные сведения о развертывании см. в следующих статьях:

- [Развертывание доменных служб Active Directory](../../ad-ds/deploy/AD-DS-Deployment.md)
- [Развертывание AD FS](../AD-FS-Deployment.md)

Пример основан на существующем образце OBO в Azure, созданном с помощью Витторио Берточчи и доступен [здесь](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof). Выполните инструкции по клонированию проекта на компьютере разработки и создайте копию примера, чтобы начать работу с.

## <a name="clone-or-download-this-repository"></a>Клонирование или скачивание этого репозитория

Из оболочки или командной строки:

```
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof.git
```

## <a name="modifying-the-sample"></a>Изменение образца

После открытия решения Вебапи-онбехалфоф-дотнет. sln вы увидите, что в решении есть два проекта

* **ToDoListClient**: это будет выступать в роли клиента OpenID Connect, с которым будет осуществляться взаимодействие пользователя.
* **ToDoListService**. это будет приложение или служба сервера среднего уровня, которые будут взаимодействовать с другим серверным WebAPI OBO, прошедшим проверку подлинности пользователя

Как видите, нам потребуется добавить еще один проект, который будет использоваться в качестве ресурса, к которому будет обращаться ToDoListService среднего уровня.

### <a name="configuring-ad-fs-for-the-client-and-webserver-app"></a>Настройка AD FS для клиентского и серверного приложений

В текущей форме примера проверка подлинности настроена для работы с Azure AD. Мы хотим изменить механизм проверки подлинности и направить его на AD FS, развернутый локально. Для этого необходимо настроить AD FS, чтобы распознать клиентское и серверное приложение в примере.

**Создание группы приложений**

Откройте консоль управления AD FS Management MMC и добавьте новую группу приложений. Выберите шаблон собственный — приложение-WebAPI.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO2.PNG)

Нажмите кнопку Далее, чтобы получить сведения о клиентском приложении. Присвойте подходящее имя клиентскому приложению в AD FS. Скопируйте идентификатор клиента и сохраните его там, где вы можете получить доступ позже, так как это потребуется в конфигурации приложения в Visual Studio.

>Примечание. URI перенаправления может быть любым произвольным URI, так как он в действительности не используется в собственных клиентах.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO11.PNG)

Нажмите кнопку Далее, и появится страница с информацией о WebAPI. Укажите подходящее имя для записи AD FS WebAPI и введите универсальный код ресурса (URI) перенаправления в качестве URI, который вы видите в Visual Studio для ToDoListService

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO16.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO18.PNG)

Нажмите кнопку Далее, и вы увидите страницу Выбор политики управления доступом. Убедитесь, что в разделе Политика отображается «разрешение всем».

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO1.PNG)

Нажмите кнопку Далее, и появится страница Настройка разрешений приложения. На этой странице Выберите разрешенные области как OpenID Connect (выбрано по умолчанию) и user_impersonation. Область "user_impersonation" необходима для успешного запроса маркера доступа от имени AD FS.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO12.PNG)

Нажмите кнопку Далее, чтобы отобразить страницу Сводка. Пройдите остальные шаги мастера и завершите настройку.

Чтобы включить проверку подлинности от имени, необходимо убедиться, что AD FS возвращает клиенту маркер доступа с областью user_impersonation. Измените выдачу утверждений для Тодолистсервицевебапи, чтобы включить следующие три настраиваемых правила:

```
@RuleName = "All claims"
c:[]
=> issue(claim = c);

@RuleName = "Issue user_impersonation scope"
=> issue(Type = "http://schemas.microsoft.com/identity/claims/scope", Value = "user_impersonation");
```

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO10.PNG)

**Добавление ToDoListService в качестве клиента в группу приложений**

На этом этапе необходимо сделать дополнительную запись в AD FS, чтобы приложение-сервер действовало как клиент, а не как ресурс. Откройте только что созданную группу приложений и щелкните Добавить приложение.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO15.PNG)

Отобразится страница "Добавление нового приложения в Мисамплеграуп". На этой странице выберите "серверное приложение или веб-сайт" в качестве автономного приложения.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO19.PNG)

Нажмите кнопку Далее. Откроется страница с информацией о приложении. Укажите подходящее имя для записи конфигурации в разделе Имя. Убедитесь, что идентификатор клиента совпадает с идентификатором для Тодолистсервицевебапи.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO20.PNG)

Нажмите кнопку Далее. Откроется страница, на которой можно настроить учетные данные приложения. Щелкните "создать общий секрет". Появится автоматически созданный секрет. Скопируйте секрет в нужное расположение, так как это потребуется при настройке ToDoListService в Visual Studio.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO17.PNG)

Нажмите кнопку Далее и завершите работу мастера.

### <a name="modifying-the-todolistclient-code"></a>Изменение кода ToDoListClient

#### <a name="modify-the-application-config"></a>Изменение конфигурации приложения

Перейдите в проект ToDoListClient в решении WebAPI-OnBehalfOf-DotNet. Откройте файл App.config и внесите следующие изменения.

* Закомментируйте запись ключа клиента Ida:
* Для Ida: RedirectURI введите произвольный URI, указанный при настройке MySampleGroup_ClientApplication в AD FS.
* Для ключа Ida: ClientID укажите идентификатор клиента, который AD FS был задан при настройке MySampleGroup_ClientApplication.
* Для Ida: Тодолистресаурцеид укажите идентификатор ресурса, который вы присвоили при настройке Тодолистсервицевебапи в AD FS
* Закомментируйте ключ Ida: Аадинстанце
* Для Ida: Тодолистбасеаддресс введите идентификатор ресурса Тодолистсервицевебапи. Он будет использоваться при вызове ToDoList WebAPI.
* Добавьте ключ Ida: Authority и укажите значение в качестве URI для AD FS.

Представление **appSettings** в App.Config должно выглядеть следующим образом:

```
<appSettings>
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />-->
    <add key="ida:ClientId" value="c7f7b85c-497c-4589-877f-b17a0bd13398" />
    <add key="ida:RedirectUri" value="https://arbitraryuri.com/" />
    <add key="ida:TodoListResourceId" value="https://localhost:44321/" />
    <!--<add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->
    <add key="ida:TodoListBaseAddress" value="https://localhost:44321" />
    <add key="ida:Authority" value="https://fs.anandmsft.com/adfs/"/>
</appSettings>
```

#### <a name="modifying-the-code"></a>Изменение кода

**MainWindow.xaml.cs**

Закомментируйте строку, считывающую сведения о клиенте, из конфигурации приложения

```
//private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
//private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
```

Измените значение центра строк на

```
private static string authority = ConfigurationManager.AppSettings["ida:Authority"];
```

Измените код для чтения правильных значений Тодолистресаурцеид и Тодолистбасеаддресс

```
private static string todoListResourceId = ConfigurationManager.AppSettings["ida:TodoListResourceId"];
private static string todoListBaseAddress = ConfigurationManager.AppSettings["ida:TodoListBaseAddress"];
```

В функции MainWindow () измените инициализацию authcontext следующим образом:

```
authContext = new AuthenticationContext(authority, false);
```

### <a name="adding-the-backend-resource"></a>Добавление серверного ресурса

Чтобы завершить поток "от имени", необходимо создать серверный ресурс, к которому ToDoListService будет обращаться от имени пользователя, прошедшего проверку подлинности. Выбор серверного ресурса может отличаться в зависимости от требования, но в этом примере можно создать базовый WebAPI.

* Щелкните правой кнопкой мыши решение "WebAPI-OnBehalfOf-DotNet" в обозревателе решений и выберите Добавить-> новый проект.
* Выбор шаблона веб-приложения ASP.NET

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO4.PNG)

* В следующем запросе щелкните "изменить проверку подлинности".
* Выберите "рабочие и учебные учетные записи", а затем в раскрывающемся списке справа выберите "локальный".
* Введите путь federationmetadata.xml для развертывания AD FS и укажите универсальный код ресурса (URI) приложения (в дальнейшем укажите универсальный код ресурса) и нажмите кнопку ОК, чтобы добавить проект в решение.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO9.PNG)

* Щелкните правой кнопкой мыши контроллеры в обозревателе решений в созданном новом проекте. Выберите "добавить-> контроллер"
* В области выбора шаблона выберите "контроллер веб-API 2-Empty" и нажмите кнопку ОК.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO3.PNG)

* Присвойте контроллеру соответствующее имя.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO13.PNG)

* Добавьте следующий код в контроллер:

    ```cs
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Http;
        namespace WebAPIOBO.Controllers
        {
            [Authorize]
            public class WebAPIOBOController : ApiController
            {
                public IHttpActionResult Get()
                {
                    return Ok($"WebAPI via OBO (user: {User.Identity.Name}");
                }
            }
        }
    ```

Этот код будет просто возвращать строку, когда кто-то помещает запрос GET для WebAPI Вебапиобо

### <a name="adding-the-new-backend-webapi-to-ad-fs"></a>Добавление новой серверной WebAPI в AD FS

Откройте группу приложений Мисамплеграуп. Щелкните Добавить приложение и выберите шаблон веб-API и нажмите кнопку Далее.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO6.PNG)

На странице Настройка веб-API укажите соответствующее имя для записи WebAPI и идентификатора. Идентификатор должен быть значением URL-адреса SSL из проекта Вебапиобо в Visual Studio (аналогично тому, что мы делали для Баккендвебапиадфсадд).

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO8.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO7.PNG)

Продолжайте работу с мастером так же, как и при настройке ToDoListService WebAPI. В конце группы приложений должна выглядеть следующим образом:

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO5.PNG)

### <a name="modifying-the-todolistservice-code"></a>Изменение кода ToDoListService

#### <a name="modifying-the-application-config"></a>Изменение конфигурации приложения

* Открытие файла Web.config
* Измените следующие ключи:

| Ключ | Значение |
|:-|:-|
| IDA: аудитория | Идентификатор ToDoListService, заданный для AD FS при настройке ToDoListService WebAPI, например https://localhost:44321/ |
| IDA: ClientID | Идентификатор ToDoListService, заданный для AD FS при настройке ToDoListService WebAPI, например <https://localhost:44321/> </br>**Очень важно, чтобы Ida: аудитория и Ida: ClientID совпадали друг с другом.** |
| ida:ClientSecret | Это секрет, который AD FS создан при настройке клиента ToDoListService в AD FS |
| IDA: Адфсметадатаендпоинт | Это URL-адрес метаданных AD FS, например https://fs.anandmsft.com/federationmetadata/2007-06/federationmetadata.xml |
| IDA: Обовебапибасе | Это базовый адрес, который будет использоваться для вызова API серверной части, например https://localhost:44300 |
| ida:Authority | Это URL-адрес службы AD FS, например https://fs.anandmsft.com/adfs/ |

Все остальные ключи Ida: XXXXXXX в узле **appSettings** можно закомментировать или удалить.

#### <a name="change-authentication-from-azure-ad-to-ad-fs"></a>Изменение проверки подлинности Azure AD на AD FS

* Откройте файл Startup.Auth.cs
* Удалите следующий код

    ```
    app.UseWindowsAzureActiveDirectoryBearerAuthentication(
    new WindowsAzureActiveDirectoryBearerAuthenticationOptions
    {
        Audience = ConfigurationManager.AppSettings["ida:Audience"],
        Tenant = ConfigurationManager.AppSettings["ida:Tenant"],
        TokenValidationParameters = new TokenValidationParameters{ SaveSigninToken = true }
    });
    ```

    на

    ```
    app.UseActiveDirectoryFederationServicesBearerAuthentication(
    new ActiveDirectoryFederationServicesBearerAuthenticationOptions
    {
        MetadataEndpoint = ConfigurationManager.AppSettings["ida:AdfsMetadataEndpoint"],
        TokenValidationParameters = new TokenValidationParameters()
    {
        SaveSigninToken = true,
        ValidAudience = ConfigurationManager.AppSettings["ida:Audience"]
    }
    });
    ```

#### <a name="modifying-the-todolistcontroller"></a>Изменение ToDoListController

Добавьте ссылку на System. Web. Extensions. Измените члены класса, заменив приведенный ниже код.

```
//
// The Client ID is used by the application to uniquely identify itself to Azure AD.
// The App Key is a credential used by the application to authenticate to Azure AD.
// The Tenant is the name of the Azure AD tenant in which this application is registered.
// The AAD Instance is the instance of Azure, for example public Azure or Azure China.
// The Authority is the sign-in URL of the tenant.
//
private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
private static string appKey = ConfigurationManager.AppSettings["ida:AppKey"];

//
// To authenticate to the Graph API, the app needs to know the Grah API's App ID URI.
// To contact the Me endpoint on the Graph API we need the URL as well.
//
private static string graphResourceId = ConfigurationManager.AppSettings["ida:GraphResourceId"];
private static string graphUserUrl = ConfigurationManager.AppSettings["ida:GraphUserUrl"];
private const string TenantIdClaimType = "https://schemas.microsoft.com/identity/claims/tenantid";
```

на

```
//
// The Client ID is used by the application to uniquely identify itself to Azure AD.
// The client secret is the credentials for the WebServer Client

private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
private static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

// Base address of the WebAPI
private static string OBOWebAPIBase = ConfigurationManager.AppSettings["ida:OBOWebAPIBase"];
```

**Изменение утверждения, используемого для имени**

В AD FS мы выдающими утверждение Нмае, но не выдаете утверждение NameIdentifier. В примере используется NameIdentifier для уникального ключа в элементах ToDo. Для простоты можно безопасно удалить NameIdentifier с утверждением имени в коде. Найдите и замените все вхождения NameIdentifier именем.

**Изменение процедуры POST и Каллграфапионбехалфофусер ()**

Скопируйте и вставьте приведенный ниже код в ToDoListController.cs и замените код для POST и Каллграфапионбехалфофусер.

```
// POST api/todolist
public async Task Post(TodoItem todo)
{
    if (!ClaimsPrincipal.Current.FindFirst("https://schemas.microsoft.com/identity/claims/scope").Value.Contains("user_impersonation"))
        {
        throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found" });
        }

//
// Call the WebAPIOBO On Behalf Of the user who called the To Do list web API.
//

    string augmentedTitle = null;
    string custommessage = await CallGraphAPIOnBehalfOfUser();

    if (custommessage != null)
        {
            augmentedTitle = String.Format("{0}, Message: {1}", todo.Title, custommessage);
        }
        else
        {
            augmentedTitle = todo.Title;
        }

      if (null != todo && !string.IsNullOrWhiteSpace(todo.Title))
        {
            db.TodoItems.Add(new TodoItem { Title = augmentedTitle, Owner = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value });
            db.SaveChanges();
        }
      }

      public static async Task<string> CallGraphAPIOnBehalfOfUser()
      {
        string accessToken = null;
        AuthenticationResult result = null;
        AuthenticationContext authContext = null;
        HttpClient httpClient = new HttpClient();
        string custommessage = "";

//
// Use ADAL to get a token On Behalf Of the current user.  To do this we will need:
// The Resource ID of the service we want to call.
// The current user's access token, from the current request's authorization header.
// The credentials of this application.
// The username (UPN or email) of the user calling the API
//

        ClientCredential clientCred = new ClientCredential(clientId, clientSecret);
        var bootstrapContext = ClaimsPrincipal.Current.Identities.First().BootstrapContext as System.IdentityModel.Tokens.BootstrapContext;
        string userName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn) != null ? ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value : ClaimsPrincipal.Current.FindFirst(ClaimTypes.Email).Value;
        string userAccessToken = bootstrapContext.Token;
        UserAssertion userAssertion = new UserAssertion(bootstrapContext.Token, "urn:ietf:params:oauth:grant-type:jwt-bearer", userName);

        string userId = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
        authContext = new AuthenticationContext(authority, false);

        // In the case of a transient error, retry once after 1 second, then abandon.
        // Retrying is optional.  It may be better, for your application, to return an error immediately to the user and have the user initiate the retry.
        bool retry = false;
        int retryCount = 0;

        do
          {
              retry = false;
              try
                {
                    result = await authContext.AcquireTokenAsync(OBOWebAPIBase, clientCred, userAssertion);
                    //result = await authContext.AcquireTokenAsync(...);
                    accessToken = result.AccessToken;
                }
              catch (AdalException ex)
                {
                    if (ex.ErrorCode == "temporarily_unavailable")
                    {
                        // Transient error, OK to retry.
                        retry = true;
                        retryCount++;
                        Thread.Sleep(1000);
                    }
                }
          } while ((retry == true) && (retryCount < 1));

        if (accessToken == null)
          {
              // An unexpected error occurred.
              return (null);
          }

        // Once the token has been returned by ADAL, add it to the http authorization header, before making the call to access the To Do list service.
        httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

        // Call the WebAPIOBO.
        HttpResponseMessage response = await httpClient.GetAsync(OBOWebAPIBase + "/api/WebAPIOBO");


        if (response.IsSuccessStatusCode)
          {
              // Read the response and databind to the GridView to display To Do items.
              string s = await response.Content.ReadAsStringAsync();
              JavaScriptSerializer serializer = new JavaScriptSerializer();
              custommessage = serializer.Deserialize<string>(s);
              return custommessage;
          }
        else
          {
              custommessage = "Unsuccessful OBO operation : " + response.ReasonPhrase;
          }
        // An unexpected error occurred calling the Graph API.  Return a null profile.
        return (null);
    }
```

## <a name="running-the-solution"></a>Запуск решения

По умолчанию Visual Studio настроен для запуска одного проекта при нажатии клавиши Отладка для запуска.

* Щелкните решение правой кнопкой мыши и выберите пункт Свойства.
* На странице Свойства выберите несколько запускаемых проектов и измените действие на начало для всех трех записей.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO14.PNG)

Нажмите клавишу F5 и выполните решение.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO24.PNG)

Нажмите кнопку Вход. Появится запрос на вход с помощью AD FS

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO25.PNG)

После входа добавьте элемент ToDo в список. В фоновом режиме мы будем выполнять операцию POST к ToDoListService, которая еще больше выполняет запись в веб-API Вебапиобо.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO26.PNG)

При успешной работе вы увидите, что элемент был добавлен в список с дополнительным сообщением из внутреннего веб-API, к которому осуществлялся доступ с помощью OBO auth-Flow.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO27.PNG)

Вы также можете просмотреть подробные трассировки на Fiddler. Запустите Fiddler и включите расшифровку по протоколу HTTPS. Вы видите, что мы делаем два запроса к конечной точке/адфс/оаутинклудес.
В первом взаимодействии мы представим код доступа к конечной точке маркера и получаем маркер доступа для https://localhost:44321/ ![ AD FS OBO.](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO22.PNG)

Во втором взаимодействии с конечной точкой маркера можно увидеть, что у нас есть **requested_token_use** в качестве **on_behalf_of** и мы используем маркер доступа, полученный для веб-службы среднего уровня, т. е. https://localhost:44321/ утверждение для получения маркера "от имени".
![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO23.PNG)

## <a name="next-steps"></a>Next Steps
[Разработка AD FS](../../ad-fs/AD-FS-Development.md)
