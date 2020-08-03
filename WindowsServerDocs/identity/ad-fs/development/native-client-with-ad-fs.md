---
title: Создание собственного клиентского приложения с помощью общедоступных клиентов OAuth с AD FS 2016 или более поздней версии
description: Пошаговое руководство, содержащее инструкции по созданию собственного клиентского приложения с помощью общедоступных клиентов OAuth и AD FS 2016 или более поздней версии.
author: billmath
ms.author: billmath
ms.reviewer: anandy
manager: mtillman
ms.date: 07/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.openlocfilehash: cecffe6ae789c4a7c8c9ff382e83d84ade8ef018
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519853"
---
# <a name="build-a-native-client-application-using-oauth-public-clients-with-ad-fs-2016-or-later"></a>Создание собственного клиентского приложения с помощью общедоступных клиентов OAuth с AD FS 2016 или более поздней версии

## <a name="overview"></a>Обзор

В этой статье показано, как создать собственное приложение, взаимодействующее с веб-API, защищенным с помощью AD FS 2016 или более поздней версии.

1. Приложение .NET TodoListClient WPF использует Библиотека проверки подлинности Active Directory (ADAL) для получения маркера доступа JWT из Azure Active Directory (Azure AD) по протоколу OAuth 2,0.
2. Маркер доступа используется в качестве токена носителя для проверки подлинности пользователя при вызове конечной точки/тодолист веб-API TodoListService.
 Мы будем использовать пример приложения для Azure AD, а затем изменим его для AD FS 2016 или более поздней версии.

![Обзор приложения](media/native-client-with-ad-fs-2016/appoverview.png)

## <a name="pre-requisites"></a>Предварительные требования
Ниже приведен список предварительных требований, которые необходимы перед завершением этого документа. В этом документе предполагается, что AD FS установлен и создана AD FS ферма.

* Клиентские средства GitHub
* AD FS в Windows Server 2016 или более поздней версии
* Visual Studio 2013 или более поздней версии

## <a name="creating-the-sample-walkthrough"></a>Создание примера пошагового руководства

### <a name="create-the-application-group-in-ad-fs"></a>Создайте группу приложений в AD FS

1. В AD FS управления щелкните правой кнопкой мыши **группы приложений** и выберите команду **Добавить группу приложений**.

2. В мастере групп приложений в поле Имя введите любое предпочтительное имя, например Нативетодолистаппграуп. Выберите **собственное приложение, осуществляющее доступ к шаблону веб-API** . Щелкните **Далее**.
 ![Добавить группу приложений](media/native-client-with-ad-fs-2016/addapplicationgroup1.png)

3. На странице **приложение машинного кода** запишите идентификатор, созданный AD FS. Это идентификатор, с помощью которого AD FS будет распознавать общедоступное клиентское приложение. Скопируйте значение **идентификатора клиента** . Он будет использоваться позже в качестве значения для **Ida: ClientID** в коде приложения. Если вы хотите, можно указать здесь любой настраиваемый идентификатор. URI перенаправления — любое произвольное значение, например, размещение https://ToDoListClient ![ собственного приложения](media/native-client-with-ad-fs-2016/addapplicationgroup2.png)

4. На странице **Настройка веб-API** задайте значение идентификатора для веб-API. В этом примере это должно быть значение **URL-адреса SSL** , на котором должно выполняться веб-приложение. Это значение можно получить, щелкнув Свойства проекта Тулистсервер в решении. Позже это будет использоваться как значение **TODO: тодолистресаурцеид** в **App.config** файле собственного клиентского приложения, а также как **TODO: тодолистбасеаддресс**.
![Веб-интерфейс API](media/native-client-with-ad-fs-2016/addapplicationgroup3.png)

5. Используйте **политику применения политики управления доступом** и **Настройте разрешения приложения** с использованием значений по умолчанию на месте. Страница сводки должна выглядеть следующим образом.
![Сводка](media/native-client-with-ad-fs-2016/addapplicationgroupsummary.png)

Нажмите кнопку Далее, а затем завершите работу мастера.

### <a name="add-the-nameidentifier-claim-to-the-list-of-claims-issued"></a>Добавление утверждения NameIdentifier в список выданных утверждений
Демонстрационное приложение использует значение в утверждении NameIdentifier в различных местах. В отличие от Azure AD, AD FS не выдает утверждение NameIdentifier по умолчанию. Поэтому необходимо добавить правило утверждений, чтобы выдать утверждение NameIdentifier, чтобы приложение может использовать правильное значение. В этом примере заданное имя пользователя выдается как значение NameIdentifier для пользователя в маркере.
Чтобы настроить правило для утверждений, откройте только что созданную группу приложений и дважды щелкните веб-API. Выберите вкладку Правила преобразования выдачи, а затем нажмите кнопку Добавить правило. В поле Тип правила утверждения выберите настраиваемое правило утверждения, а затем добавьте правило утверждения, как показано ниже.

```
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
 => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier"), query = ";givenName;{0}", param = c.Value);
```

![Правило для утверждений NameIdentifier](media/native-client-with-ad-fs-2016/addnameidentifierclaimrule.png)

### <a name="modify-the-application-code"></a>Изменение кода приложения

В этом разделе описывается, как скачать пример веб-API и изменить его в Visual Studio.   Мы будем использовать пример Azure AD, приведенный [здесь](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop).

Чтобы скачать пример проекта, используйте Git Bash и введите следующую команду:

```
git clone https://github.com/Azure-Samples/active-directory-dotnet-native-desktop
```

#### <a name="modify-todolistclient"></a>Изменить ToDoListClient

Этот проект в решении представляет собственное клиентское приложение. Необходимо убедиться, что клиентское приложение знает:

1. Куда перейти, чтобы получить пользователя с проверкой подлинности при необходимости?
2. Каков идентификатор, который клиент должен предоставить в центре проверки подлинности (AD FS)?
3. Идентификатор ресурса, для которого запрашивается маркер доступа?
4. Каков базовый адрес веб-API?

Чтобы получить приведенные выше сведения в собственном клиентском приложении, необходимо внести следующие изменения в код.

**App.config**

* Добавьте ключ **Ida: Authority** со значением, описывающим службу AD FS. Например https://fs.contoso.com/adfs/.
* Измените **Ida: ClientID** Key на значение из **идентификатора клиента** на странице **приложения Native** во время создания группы приложений в AD FS. Например, 3f07368b-6efd-4f50-A330-d93853f4c855
* Измените значение **TODO: TODO: тодолистресаурцеид** со значением **идентификатора** на странице **Настройка веб-API** во время создания группы приложений в AD FS. Например https://localhost:44321/.
* Измените значение **TODO: тодолистбасеаддресс** со значением **идентификатора** на странице **Настройка веб-API** во время создания группы приложений в AD FS. Например https://localhost:44321/.
* Задайте значение **Ida: RedirectUri** со ЗНАЧЕНИЕМ из **URI перенаправления** на странице **приложения Native** во время создания группы приложений в AD FS. Например https://ToDoListClient.
* Для удобства чтения можно удалить или закомментировать ключ для **Ida: клиент** и **Ida: аадинстанце**.

  ![Конфигурация приложения](media/native-client-with-ad-fs-2016/app_configfile.PNG)

**MainWindow.xaml.cs**

* Закомментируйте строку для Аадинстанце, как показано ниже

    `// private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];`

* Добавьте значение для центра сертификации, как показано ниже.

    `private static string authority = ConfigurationManager.AppSettings["ida:Authority"];`

* Удалите строку для создания значения **Authority** из аадинстанце и клиента.

    `private static string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);`

* В функции **MainWindow**измените создание экземпляра authContext на

   `authContext = new AuthenticationContext(authority,false);`

    ADAL не поддерживает проверку AD FS как полномочия, поэтому необходимо передать флаг false для параметра Валидатеаусорити.

  ![Главное окно](media/native-client-with-ad-fs-2016/mainwindow.PNG)

#### <a name="modify-todolistservice"></a>Изменить TodoListService
Два файла нуждаются в изменениях в этом проекте — Web.config и Startup.Auth.cs. Для получения правильных значений параметров необходимо Web.Config изменения. Startup.Auth.cs изменения необходимы для настройки WebAPI для проверки подлинности в AD FS, а не Azure AD.

**Web.config**

* Закомментируйте ключ **Ida: клиент** , так как он не нужен
* Добавьте ключ для **Ida: Authority** со значением, указывающим полное доменное имя службы федерации, напримерhttps://fs.contoso.com/adfs/
* Измените key **Ida: аудитория** на значение идентификатора веб-API, указанного на странице **Настройка веб-API** во время добавления группы приложений в AD FS.
* Добавьте key **Ida: адфсметадатаендпоинт** со значением, соответствующим URL-адресу метаданных федерации службы AD FS, например:https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

![Веб-конфигурация](media/native-client-with-ad-fs-2016/webconfig.PNG)

**Startup.Auth.cs**

Измените функцию Конфигуреаус, как показано ниже.

```
    public void ConfigureAuth(IAppBuilder app)
    {
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
    }
```

По сути, мы настроим проверку подлинности для использования AD FS и Дополнительно предоставляем сведения о AD FS метаданных, а также для проверки маркера, что утверждение аудитории должно быть значением, ожидаемым веб-API.
Запуск приложения

1. В решении NativeClient-DotNet щелкните правой кнопкой мыши и выберите пункт Свойства. Измените запускаемый проект, как показано ниже, на несколько запускаемых проектов и задайте для параметра TodoListClient и TodoListService значение Start.
![Свойства решения](media/native-client-with-ad-fs-2016/solutionproperties.png)

2.  Нажмите клавишу F5 или выберите Отладка > продолжить в строке меню. Это приведет к запуску собственного приложения и WebAPI. Нажмите кнопку Вход в собственном приложении, чтобы открыть интерактивный вход из AD AL и перенаправить в службу AD FS. Введите учетные данные допустимого пользователя.
![Вход](media/native-client-with-ad-fs-2016/sign-in.png)

На этом шаге собственное приложение перенаправлено на AD FS и получило маркер идентификации и маркер доступа для веб-API.

3. Введите в текстовое поле элемент для Do и щелкните Добавить элемент. На этом шаге приложение переходит к веб-API, чтобы добавить элемент to do, и для этого предоставляет маркер доступа к WebAPI, полученному от AD FS. Веб-API соответствует значению аудитории, чтобы убедиться, что маркер предназначен для него, и проверяет подпись маркера с помощью сведений из метаданных федерации.

![Вход](media/native-client-with-ad-fs-2016/clienttodoadd.png)

## <a name="next-steps"></a>Next Steps
[Разработка AD FS](../../ad-fs/AD-FS-Development.md)
