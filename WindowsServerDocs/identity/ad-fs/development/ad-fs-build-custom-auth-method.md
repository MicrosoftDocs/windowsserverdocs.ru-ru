---
title: Создание пользовательского метода проверки подлинности для AD FS в Windows Server
description: В этом сценарии описывается создание пользовательского метода проверки подлинности для AD FS в Windows Server.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 05/23/2019
ms.topic: article
ms.openlocfilehash: 2a4df9738c1510aa35270fad1283b0b137aeac82
ms.sourcegitcommit: a868f7d8bb9c5becffc688fd9b75c80802af71ba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778625"
---
# <a name="build-a-custom-authentication-method-for-ad-fs-in-windows-server"></a>Создание пользовательского метода проверки подлинности для AD FS в Windows Server

В этом пошаговом руководстве приводятся инструкции по реализации пользовательского метода проверки подлинности для AD FS в Windows Server 2012 R2. Дополнительные сведения см. в разделе [Дополнительные методы проверки подлинности](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11)).

> [!WARNING]
> Пример, который можно создать здесь, предназначен &nbsp; только для образовательных целей. &nbsp;Эти инструкции предназначены для самой простой и минимальной реализации, которая может предоставить необходимые элементы модели. &nbsp; Нет серверной части проверки подлинности, обработки ошибок или данных конфигурации.

## <a name="setting-up-the-development-box"></a>Настройка поля разработки

В этом пошаговом руководстве используется Visual Studio 2012. Проект можно построить с помощью любой среды разработки, в которой можно создать класс .NET для Windows. Проект должен быть предназначен для .NET 4,5, поскольку методы **бегинаусентикатион** и **Трендаусентикатион** используют тип **System. Security. Claims. Claim**, часть .NET Framework версии 4.5. для проекта требуется одна ссылка:

| Ссылка на библиотеку DLL | Где ее найти | Обязательно для: |
|--|--|--|
| Microsoft.IdentityServer.Web.dll | Библиотека DLL находится в папке% WINDIR% ADFS на сервере Windows Server 2012 R2, на котором установлена AD FS.<p>Эта библиотека DLL должна быть скопирована на компьютер разработки и явная ссылка, созданная в проекте. | Типы интерфейсов, включая Иаусентикатионконтекст, Ипруфдата |

## <a name="create-the-provider"></a>Создание поставщика

1. В Visual Studio 2012: выберите файл->создать->проект...

2. Выберите Библиотека классов и убедитесь, что вы используете .NET 4,5.

    ![создание поставщика](media/ad-fs-build-custom-auth-method/Dn783423.71a57ae1-d53d-462b-a846-5b3c02c7d3f2(MSDN.10).jpg "создание поставщика")

3. Создайте копию **Microsoft.IdentityServer.Web.dll** из служб ADFS% WINDIR% на сервере Windows Server 2012 R2, где AD FS установлен, и вставьте его в папку проекта на компьютере разработчика.

4. В **Обозреватель решений**щелкните правой кнопкой мыши **ссылки** и **Добавить ссылку...**

5. Перейдите к локальной копии **Microsoft.IdentityServer.Web.dll** и **добавьте...**

6. Нажмите кнопку **ОК** , чтобы подтвердить новую ссылку:

    ![создание поставщика](media/ad-fs-build-custom-auth-method/Dn783423.f18df353-9259-4744-b4b6-dd780ce90951(MSDN.10).jpg "создание поставщика")

    Теперь необходимо настроить разрешение всех типов, необходимых для поставщика.

7. Добавьте в проект новый класс (щелкните проект правой кнопкой мыши, **добавьте... Класс...**) и присвойте ему имя, например **мядаптер**, как показано ниже:

    ![создание поставщика](media/ad-fs-build-custom-auth-method/Dn783423.6b6a7a8b-9d66-40c7-8a86-a2e3b9e14d09(MSDN.10).jpg "создание поставщика")

8. В новом файле MyAdapter.cs замените существующий код следующим:

    ```
    using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Text;
        using System.Threading.Tasks;
        using System.Globalization;
        using System.IO;
        using System.Net;
        using System.Xml.Serialization;
        using Microsoft.IdentityServer.Web.Authentication.External;
        using Claim = System.Security.Claims.Claim;

        namespace MFAadapter
         {
         class MyAdapter : IAuthenticationAdapter
         {
         public IAuthenticationAdapterMetadata Metadata
         {
         //get { return new <instance of IAuthenticationAdapterMetadata derived class>; }
         }

         public IAdapterPresentation BeginAuthentication(Claim identityClaim, HttpListenerRequest request, IAuthenticationContext authContext)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         public bool IsAvailableForUser(Claim identityClaim, IAuthenticationContext authContext)
         {
         return true; //its all available for now

         }

         public void OnAuthenticationPipelineLoad(IAuthenticationMethodConfigData configData)
         {
         //this is where AD FS passes us the config data, if such data was supplied at registration of the adapter

         }

         public void OnAuthenticationPipelineUnload()
         {

         }

         public IAdapterPresentation OnError(HttpListenerRequest request, ExternalAuthenticationException ex)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         }
         }

10. We are not ready to build yet... there are two more interfaces to go.

    Add two more classes to your project: one is for the metadata, and the other for the presentation form.  You can add these within the same file as the class above.

        class MyMetadata : IAuthenticationAdapterMetadata
         {

         }

         class MyPresentationForm : IAdapterPresentationForm
         {

         }

11. Next, you can add the required members for each.First, the metadata (with helpful inline comments)

        class MyMetadata : IAuthenticationAdapterMetadata
         {
         //Returns the name of the provider that will be shown in the AD FS management UI (not visible to end users)
         public string AdminName
         {
         get { return "My Example MFA Adapter"; }
         }

         //Returns an array of strings containing URIs indicating the set of authentication methods implemented by the adapter 
         /// AD FS requires that, if authentication is successful, the method actually employed will be returned by the
         /// final call to TryEndAuthentication(). If no authentication method is returned, or the method returned is not
         /// one of the methods listed in this property, the authentication attempt will fail.
         public virtual string[] AuthenticationMethods 
         {
         get { return new[] { "http://example.com/myauthenticationmethod1", "http://example.com/myauthenticationmethod2" }; }
         }

         /// Returns an array indicating which languages are supported by the provider. AD FS uses this information
         /// to determine the best language\locale to display to the user.
         public int[] AvailableLcids
         {
         get
         {
         return new[] { new CultureInfo("en-us").LCID, new CultureInfo("fr").LCID};
         }
         }

         /// Returns a Dictionary containing the set of localized friendly names of the provider, indexed by lcid. 
         /// These Friendly Names are displayed in the "choice page" offered to the user when there is more than 
         /// one secondary authentication provider available.
         public Dictionary<int, string> FriendlyNames
         {
         get
         {
         Dictionary<int, string> _friendlyNames = new Dictionary<int, string>();
         _friendlyNames.Add(new CultureInfo("en-us").LCID, "Friendly name of My Example MFA Adapter for end users (en)");
         _friendlyNames.Add(new CultureInfo("fr").LCID, "Friendly name translated to fr locale");
         return _friendlyNames;
         }
         }

         /// Returns a Dictionary containing the set of localized descriptions (hover over help) of the provider, indexed by lcid. 
         /// These descriptions are displayed in the "choice page" offered to the user when there is more than one 
         /// secondary authentication provider available.
         public Dictionary<int, string> Descriptions
         {
         get 
         {
         Dictionary<int, string> _descriptions = new Dictionary<int, string>();
         _descriptions.Add(new CultureInfo("en-us").LCID, "Description of My Example MFA Adapter for end users (en)");
         _descriptions.Add(new CultureInfo("fr").LCID, "Description translated to fr locale");
         return _descriptions; 
         }
         }

         /// Returns an array indicating the type of claim that the adapter uses to identify the user being authenticated.
         /// Note that although the property is an array, only the first element is currently used.
         /// MUST BE ONE OF THE FOLLOWING
         /// "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"
         /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"
         /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"
         /// "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"
         public string[] IdentityClaims
         {
         get { return new[] { "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" }; }
         }

         //All external providers must return a value of "true" for this property.
         public bool RequiresIdentity
         {
         get { return true; }
         }
        }
    ```

    Теперь вы можете нажать клавишу F12 (щелкните правой кнопкой мыши — переход к определению) на Иаусентикатионадаптер, чтобы увидеть набор требуемых членов интерфейса.

    Далее можно выполнить простую реализацию этих методов.

9. Замените все содержимое класса следующим:

    ```
    namespace MFAadapter
    {
    class MyAdapter : IAuthenticationAdapter
    {
    public IAuthenticationAdapterMetadata Metadata
    {
    //get { return new <instance of IAuthenticationAdapterMetadata derived class>; }
    }

    public IAdapterPresentation BeginAuthentication(Claim identityClaim, HttpListenerRequest request, IAuthenticationContext authContext)
    {
    //return new instance of IAdapterPresentationForm derived class
    }

    public bool IsAvailableForUser(Claim identityClaim, IAuthenticationContext authContext)
    {
    return true; //its all available for now
    }

    public void OnAuthenticationPipelineLoad(IAuthenticationMethodConfigData configData)
    {
    //this is where AD FS passes us the config data, if such data was supplied at registration of the adapter
    }

    public void OnAuthenticationPipelineUnload()
    {
     }

    public IAdapterPresentation OnError(HttpListenerRequest request, ExternalAuthenticationException ex)
    {
    //return new instance of IAdapterPresentationForm derived class
    }

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
    {
    //return new instance of IAdapterPresentationForm derived class
            }
        }
    }
    ```

1. Мы еще не готовы к сборке... Есть еще два интерфейса для перехода.

    Добавьте в проект еще два класса: один — для метаданных, другой — для формы представления. Их можно добавить в тот же файл, что и приведенный выше класс.

    ```
    class MyMetadata : IAuthenticationAdapterMetadata
    {
    }
    class MyPresentationForm : IAdapterPresentationForm
    {
    }
    ```

2. Далее можно добавить необходимые элементы для каждого из них. Во-первых, метаданные (с полезными встроенными комментариями)

    ```
    class MyMetadata : IAuthenticationAdapterMetadata
    {
    //Returns the name of the provider that will be shown in the AD FS management UI (not visible to end users)
    public string AdminName
    {
    get { return "My Example MFA Adapter"; }
    }

    //Returns an array of strings containing URIs indicating the set of authentication methods implemented by the adapter
    /// AD FS requires that, if authentication is successful, the method actually employed will be returned by the
    /// final call to TryEndAuthentication(). If no authentication method is returned, or the method returned is not
    /// one of the methods listed in this property, the authentication attempt will fail.
    public virtual string[] AuthenticationMethods
    {
    get { return new[] { "http://example.com/myauthenticationmethod1", "http://example.com/myauthenticationmethod2" }; }
    }

    /// Returns an array indicating which languages are supported by the provider. AD FS uses this information
    /// to determine the best languagelocale to display to the user.
    public int[] AvailableLcids
    {
    get
    {
    return new[] { new CultureInfo("en-us").LCID, new CultureInfo("fr").LCID};
    }
    }

    /// Returns a Dictionary containing the set of localized friendly names of the provider, indexed by lcid.
    /// These Friendly Names are displayed in the "choice page" offered to the user when there is more than
    /// one secondary authentication provider available.
    public Dictionary<int, string> FriendlyNames
    {
    get
    {
    Dictionary<int, string> _friendlyNames = new Dictionary<int, string>();
    _friendlyNames.Add(new CultureInfo("en-us").LCID, "Friendly name of My Example MFA Adapter for end users (en)");
    _friendlyNames.Add(new CultureInfo("fr").LCID, "Friendly name translated to fr locale");
    return _friendlyNames;
    }
    }

    /// Returns a Dictionary containing the set of localized descriptions (hover over help) of the provider, indexed by lcid.
    /// These descriptions are displayed in the "choice page" offered to the user when there is more than one
    /// secondary authentication provider available.
    public Dictionary<int, string> Descriptions
    {
    get
    {
    Dictionary<int, string> _descriptions = new Dictionary<int, string>();
    _descriptions.Add(new CultureInfo("en-us").LCID, "Description of My Example MFA Adapter for end users (en)");
    _descriptions.Add(new CultureInfo("fr").LCID, "Description translated to fr locale");
    return _descriptions;
    }
    }

    /// Returns an array indicating the type of claim that the adapter uses to identify the user being authenticated.
    /// Note that although the property is an array, only the first element is currently used.
    /// MUST BE ONE OF THE FOLLOWING
    /// "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"
    /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"
    /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"
    /// "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"
    public string[] IdentityClaims
    {
    get { return new[] { "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" }; }
    }

    //All external providers must return a value of "true" for this property.
    public bool RequiresIdentity
    {
    get { return true; }
    }
    }
    ```

    Далее в форме презентации:

    ```
    class MyPresentationForm : IAdapterPresentationForm
    {
    /// Returns the HTML Form fragment that contains the adapter user interface. This data will be included in the web page that is presented
    /// to the cient.
    public string GetFormHtml(int lcid)
    {
    string htmlTemplate = Resources.FormPageHtml; //todo we will implement this
    return htmlTemplate;
    }

    /// Return any external resources, ie references to libraries etc., that should be included in
    /// the HEAD section of the presentation form html.
    public string GetFormPreRenderHtml(int lcid)
    {
    return null;
    }

    //returns the title string for the web page which presents the HTML form content to the end user
    public string GetPageTitle(int lcid)
    {
    return "MFA Adapter";
    }
    ```

3.  Обратите внимание на "TODO" для элемента **Resources. формпажехтмл** выше.

    Вы можете исправить это в минуту, но сначала добавим окончательные обязательные инструкции Return, основанные на вновь реализованных типах, в исходный класс Мядаптер. Для этого добавьте элементы, указанные *курсивом* , в существующую реализацию иаусентикатионадаптер:

    ```
    class MyAdapter : IAuthenticationAdapter
    {
    public IAuthenticationAdapterMetadata Metadata
    {
    //get { return new <instance of IAuthenticationAdapterMetadata derived class>; }
    get { return new MyMetadata(); }
    }

    public IAdapterPresentation BeginAuthentication(Claim identityClaim, HttpListenerRequest request, IAuthenticationContext authContext)
    {
    //return new instance of IAdapterPresentationForm derived class
    return new MyPresentationForm();
    }

    public bool IsAvailableForUser(Claim identityClaim, IAuthenticationContext authContext)
    {
    return true; //its all available for now
    }

    public void OnAuthenticationPipelineLoad(IAuthenticationMethodConfigData configData)
    {
    //this is where AD FS passes us the config data, if such data was supplied at registration of the adapter

    }

    public void OnAuthenticationPipelineUnload()
    {

    }

    public IAdapterPresentation OnError(HttpListenerRequest request, ExternalAuthenticationException ex)
    {
    //return new instance of IAdapterPresentationForm derived class
        return new MyPresentationForm();
    }

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
    {
    //return new instance of IAdapterPresentationForm derived class
    outgoingClaims = new Claim[0];
    return new MyPresentationForm();
    }

    }
    ```

13. Теперь для файла ресурсов, содержащего фрагмент HTML. Создайте в папке проекта новый текстовый файл со следующим содержимым:

       ```html
       <div id="loginArea">
        <form method="post" id="loginForm" >
        <!-- These inputs are required by the presentation framework. Do not modify or remove -->
        <input id="authMethod" type="hidden" name="AuthMethod" value="%AuthMethod%"/>
        <input id="context" type="hidden" name="Context" value="%Context%"/>
        <!-- End inputs are required by the presentation framework. -->
        <p id="pageIntroductionText">This content is provided by the MFA sample adapter. Challenge inputs should be presented below.</p>
        <label for="challengeQuestionInput" class="block">Question text</label>
        <input id="challengeQuestionInput" name="ChallengeQuestionAnswer" type="text" value="" class="text" placeholder="Answer placeholder" />
        <div id="submissionArea" class="submitMargin">
        <input id="submitButton" type="submit" name="Submit" value="Submit" onclick="return AuthPage.submitAnswer()"/>
        </div>
        </form>
        <div id="intro" class="groupMargin">
        <p id="supportEmail">Support information</p>
        </div>
        <script type="text/javascript" language="JavaScript">
        //<![CDATA[
        function AuthPage() { }
        AuthPage.submitAnswer = function () { return true; };
        //]]>
        </script></div>
       ```

14. Затем выберите **проект — \> Добавить компонент... Файл ресурсов** и назовите файловые **ресурсы**и нажмите кнопку **Добавить:**

   ![создание поставщика](media/ad-fs-build-custom-auth-method/Dn783423.3369ad8f-f65f-4f36-a6d5-6a3edbc1911a(MSDN.10).jpg "создание поставщика")

15. Затем в файле **Resources. resx** выберите **Добавить ресурс... Добавить существующий файл**. Перейдите к текстовому файлу (содержащему фрагмент HTML), сохраненному ранее.

   Убедитесь, что код Жетформхтмл правильно разрешает имя нового ресурса с помощью префикса имени файла ресурсов (RESX-файла), за которым следует имя самого ресурса:

```
    public string GetFormHtml(int lcid)
    {
    string htmlTemplate = Resources.MfaFormHtml; //Resxfilename.resourcename
    return htmlTemplate;
    }
```

   Теперь вы можете создать.

## <a name="build-the-adapter"></a>Создание адаптера

Адаптер должен быть встроен в сборку .NET со строгим именем, которую можно установить в глобальный кэш сборок (GAC) в Windows. Чтобы добиться этого в проекте Visual Studio, выполните следующие действия.

1. Щелкните правой кнопкой мыши имя проекта в обозреватель решений и выберите пункт **Свойства**.

2. На вкладке **Подписывание** установите флажок **подписать сборку** и выберите **<создать... >** в разделе **выберите файл ключа строгого имени:**  введите имя файла ключа и пароль и нажмите кнопку **ОК**. Убедитесь, что установлен флажок **подпись сборки** и снят флажок **только отложенная подпись** . Страница **подписывания** свойств должна выглядеть следующим образом:

    ![построение поставщика](media/ad-fs-build-custom-auth-method/Dn783423.0b1a1db2-d64e-4bb8-8c01-ef34296a2668(MSDN.10).jpg "построение поставщика")

3. Затем выполните сборку решения.

## <a name="deploy-the-adapter-to-your-ad-fs-test-machine"></a>Развертывание адаптера на тестовом компьютере AD FS

Прежде чем внешний поставщик можно будет вызвать с помощью AD FS, он должен быть зарегистрирован в системе. Поставщики адаптеров должны предоставить установщик, который выполняет необходимые действия по установке, включая установку в GAC, и установщик должен поддерживать регистрацию в AD FS. Если это не так, администратору необходимо выполнить приведенные ниже шаги Windows PowerShell. Эти действия можно использовать в лаборатории, чтобы включить тестирование и отладку.

### <a name="prepare-the-test-ad-fs-machine"></a>Подготовка тестового AD FS машины

Скопируйте файлы и добавьте их в глобальный кэш сборок.

1. Убедитесь, что у вас есть компьютер Windows Server 2012 R2 или виртуальная машина.

2. Установите службу роли AD FS и настройте ферму по крайней мере с одним узлом.

    Подробные инструкции по настройке сервера федерации в лабораторной среде см. в [руководстве по развертыванию Windows server 2012 R2 AD FS](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11)).

3. Скопируйте средства Gacutil.exe на сервер.

    Gacutil.exe можно найти в **файле% хомедриве% Program Files (x86) Microsoft сдксвиндовсв 8.0 абиннетфкс 4,0 Tools** на компьютере с Windows 8. Вам потребуется сам файл **gacutil.exe** , а также **1033**, **en-US**и другую локализованную папку ресурсов под расположением **средств NETFX 4,0** .

4. Скопируйте файлы поставщика (один или несколько подписанных DLL-файлов строгого имени) в то же расположение папки, что и **gacutil.exe** (расположение доступно только для удобства).

5. Добавьте DLL-файлы в глобальный кэш сборок на каждом AD FS сервере федерации в ферме:

    Пример. Использование программы командной строки GACutil.exe для добавления библиотеки DLL в глобальный кэш сборок: `C:>.gacutil.exe /if .<yourdllname>.dll`

    Чтобы просмотреть результирующую запись в GAC, сделайте следующее:`C:>.gacutil.exe /l <yourassemblyname>`

6.

### <a name="register-your-provider-in-ad-fs"></a>Регистрация поставщика в AD FS

После выполнения описанных выше условий Откройте командное окно Windows PowerShell на сервере федерации и введите следующие команды (Обратите внимание, что если используется ферма серверов федерации, использующая внутреннюю базу данных Windows, необходимо выполнить следующие команды на основном сервере федерации фермы):

1. `Register-AdfsAuthenticationProvider –TypeName YourTypeName –Name “AnyNameYouWish” [–ConfigurationFilePath (optional)]`

    Где Йоуртипенаме — имя строгого типа .NET: "Йоурдефаултнамеспаце. Йоуриаусентикатионадаптеримплементатионкласснаме, YourAssemblyName, Version = YourAssemblyVersion, Culture = Neutral, PublicKeyToken = YourPublicKeyTokenValue, processorArchitecture = MSIL"

    При этом внешний поставщик будет зарегистрирован в AD FS с именем, которое вы указали как Анинамэйаувиш выше.

2. Перезапустите службу AD FS (например, с помощью оснастки "службы Windows").

3. Выполните следующую команду: `Get-AdfsAuthenticationProvider`.

    В этом случае поставщик будет отображаться как один из поставщиков в системе.

    Пример

    ```powershell
    $typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”
    Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter”
    net stop adfssrv
    net start adfssrv
    ```

    Если служба регистрации устройств включена в среде AD FS, также выполните следующую команду PowerShell: `net start drs`

    Чтобы проверить зарегистрированный поставщик, используйте следующую команду PowerShell: `Get-AdfsAuthenticationProvider` .

    В этом случае поставщик будет отображаться как один из поставщиков в системе.

### <a name="create-the-ad-fs-authentication-policy-that-invokes-your-adapter"></a>Создание AD FS политики проверки подлинности, вызывающей адаптер

#### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>Создание политики проверки подлинности с помощью оснастки "Управление AD FS"

1. Откройте оснастку "Управление AD FS" (в меню " **Сервис** " Диспетчер сервера).

2. Щелкните **политики проверки подлинности**.

3. В центральной области в разделе **многофакторная проверка подлинности**щелкните ссылку **изменить** справа от параметра **глобальные параметры**.

4. В разделе **Выбор дополнительных методов проверки подлинности** в нижней части страницы установите флажок для админнаме поставщика. Щелкните **Применить**.

5. Чтобы предоставить "триггер" для вызова MFA с помощью адаптера, в разделе **расположения** проверьте как **экстрасеть** , так и **интрасеть**, например. Щелкните **ОК**. (Чтобы настроить триггеры для каждой проверяющей стороны, см. раздел "Создание политики проверки подлинности с помощью Windows PowerShell" ниже.)

6. Проверьте результаты с помощью следующих команд:

    Первое использование `Get-AdfsGlobalAuthenticationPolicy` . Вы должны увидеть имя поставщика как одно из значений Аддитионалаусентикатионпровидер.

    Затем используйте `Get-AdfsAdditionalAuthenticationRule` . Вы должны увидеть правила для экстрасети и интрасети, настроенные в результате выбора политики в пользовательском интерфейсе администратора.

#### <a name="create-the-authentication-policy-using-windows-powershell"></a>Создание политики проверки подлинности с помощью Windows PowerShell

1. Сначала включите поставщик в глобальной политике:

    ```powershell
    Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider “YourAuthProviderName”`
    ```

    > [!NOTE]
    > Обратите внимание, что значение, указанное для параметра Аддитионалаусентикатионпровидер, соответствует значению, указанному для параметра Name в приведенном выше командлете Register-Адфсаусентикатионпровидер и свойству Name из выходных данных командлета Get-Адфсаусентикатионпровидер.

    ```powershell
    Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider “MyMFAAdapter”`
    ```

2. Затем настройте глобальные или проверяющие правила для конкретного субъекта, чтобы активировать MFA:

   Пример 1. Создание глобального правила, требующего использования MFA для внешних запросов:
   
   ```
   PS C:\>Set-AdfsAdditionalAuthenticationRule –AdditionalAuthenticationRules 'c:[type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "http://schemas.microsoft.com/claims/multipleauthn" );'
   ```
   Пример 2. Создание правил MFA для запроса MFA для внешних запросов к конкретной проверяющей стороне. (Обратите внимание, что отдельные поставщики не могут быть подключены к отдельным проверяющим сторонам в AD FS в Windows Server 2012 R2).

    ```powershell
    PS C:\>$rp = Get-AdfsRelyingPartyTrust –Name <Relying Party Name>
    PS C:\>Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules 'c:[type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "http://schemas.microsoft.com/claims/multipleauthn" );'
    ```

### <a name="authenticate-with-mfa-using-your-adapter"></a>Проверка подлинности с помощью MFA с использованием адаптера

Наконец, выполните следующие действия, чтобы проверить адаптер:

1. Убедитесь, что AD FS глобальный первичный тип проверки подлинности настроен как проверка подлинности с помощью форм для экстрасети и интрасети (это упрощает проверку подлинности в качестве конкретного пользователя).

    1. В оснастке AD FS в разделе **политики проверки подлинности**в области **Основная проверка подлинности** щелкните **изменить** рядом с **параметром глобальные параметры**.

        1. Или просто перейдите на вкладку **Основная** в пользовательском интерфейсе **многофакторной политики** .

2. **Проверка подлинности** с помощью форм — единственный параметр, проверяемый как для экстрасети, так и для метода аутентификации в интрасети. Щелкните **ОК**.

3. Откройте HTML-страницу IDP инициировал вход (https:// <fsname> /адфс/лс/idpinitiatedsignon.htm) и выполните вход в качестве допустимого пользователя AD в тестовой среде.

4. Введите учетные данные для основной проверки подлинности.

5. Откроется страница форм MFA с примерами вопросов.

    Если настроено несколько адаптеров, вы увидите страницу выбора MFA с понятным именем выше.

    ![проверка подлинности с помощью адаптера](media/ad-fs-build-custom-auth-method/Dn783423.c98d2712-cbd3-4cb9-ac03-2838b81c4f63(MSDN.10).jpg "проверка подлинности с помощью адаптера")

    ![проверка подлинности с помощью адаптера](media/ad-fs-build-custom-auth-method/Dn783423.fd3aefc0-ef6c-4a8c-a737-4914c78ff2d2(MSDN.10).jpg "проверка подлинности с помощью адаптера")

Теперь у вас есть рабочая реализация интерфейса, и вы имеете знания о том, как работает модель. Вы можете Трим в качестве дополнительного примера для установки точек останова в Бегинаусентикатион, а также Трендаусентикатион. Обратите внимание на то, как Бегинаусентикатион выполняется при первом входе пользователя в форму MFA, в то время как Трендаусентикатион активируется при каждой отправке формы.

## <a name="update-the-adapter-for-successful-authentication"></a>Обновление адаптера для успешной проверки подлинности

Но подождите: ваш пример адаптера никогда не будет проходить проверку подлинности!  Это вызвано тем, что в коде не возвращается значение NULL для Трендаусентикатион.

Выполнив приведенные выше процедуры, вы создали базовую реализацию адаптера и добавили ее на сервер AD FS. Вы можете получить страницу форм MFA, но еще не можете пройти проверку подлинности, так как вы еще не поместили правильную логику в реализацию Трендаусентикатион. Добавим это.

Отзыв реализации Трендаусентикатион:

```
public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
{
//return new instance of IAdapterPresentationForm derived class
outgoingClaims = new Claim[0];
return new MyPresentationForm();
}
```

Давайте выполним обновление, чтобы он не всегда возвращал Мипресентатионформ (). Для этого можно создать один простой служебный метод в своем классе:

```
static bool ValidateProofData(IProofData proofData, IAuthenticationContext authContext)
{
if (proofData == null || proofData.Properties == null || !proofData.Properties.ContainsKey("ChallengeQuestionAnswer"))
{
throw new ExternalAuthenticationException("Error - no answer found", authContext);
}

if ((string)proofData.Properties["ChallengeQuestionAnswer"] == "adfabric")
{
return true;
}
else
{
return false;
}
}
```

Затем обновите Трендаусентикатион, как показано ниже:

```
public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
{
outgoingClaims = new Claim[0];
if (ValidateProofData(proofData, authContext))
{
//authn complete - return authn method
outgoingClaims = new[]
{
// Return the required authentication method claim, indicating the particulate authentication method used.
new Claim( "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod",
"http://example.com/myauthenticationmethod1" )
};
return null;
}
else
{
//authentication not complete - return new instance of IAdapterPresentationForm derived class
return new MyPresentationForm();
}
}
```

Теперь необходимо обновить адаптер на тестовом поле. Сначала необходимо отменить политику AD FS, отменять регистрацию из AD FS и перезапустить AD FS, затем удалить DLL из глобального кэша сборок, затем добавить новую DLL-файл в глобальный кэш сборок, а затем зарегистрировать ее в AD FS, перезапустить AD FS и повторно настроить политику AD FS.

## <a name="deploy-and-configure-the-updated-adapter-on-your-test-ad-fs-machine"></a>Развертывание и настройка обновленного адаптера на компьютере тестового AD FS

### <a name="clear-ad-fs-policy"></a>Очистить политику AD FS

Снимите все флажки, связанные с MFA, в пользовательском интерфейсе MFA, как показано ниже, а затем нажмите кнопку ОК.

![сброс политики](media/ad-fs-build-custom-auth-method/Dn783423.c111b4e7-5b05-413c-8b0f-222a0e91ac1f(MSDN.10).jpg "сброс политики")

### <a name="unregister-provider-windows-powershell"></a>Отмена регистрации поставщика (Windows PowerShell)

`PS C:> Unregister-AdfsAuthenticationProvider –Name “YourAuthProviderName”`

Пример:`PS C:> Unregister-AdfsAuthenticationProvider –Name “MyMFAAdapter”`

Обратите внимание, что передаваемое "имя" значение совпадает с именем "имя", предоставленным командлету Register-Адфсаусентикатионпровидер. Это также свойство Name, которое выводится из Get-Адфсаусентикатионпровидер.

Обратите внимание, что перед отменой регистрации поставщика необходимо удалить поставщик из Адфсглобалаусентикатионполици (путем очистки флажков, которые вы вернули в оснастке управления AD FS или с помощью Windows PowerShell.)

Обратите внимание, что после выполнения этой операции необходимо перезапустить службу AD FS.

### <a name="remove-assembly-from-gac"></a>Удалить сборку из GAC

1. Сначала используйте следующую команду, чтобы найти полное строгое имя записи:`C:>.gacutil.exe /l <yourAdapterAssemblyName>`

    Пример:`C:>.gacutil.exe /l mfaadapter`

2. Затем используйте следующую команду, чтобы удалить ее из глобального кэша сборок:`.gacutil /u “<output from the above command>”`

    Пример:`C:>.gacutil /u “mfaadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

### <a name="add-the-updated-assembly-to-gac"></a>Добавление обновленной сборки в глобальный кэш сборок

Сначала обязательно вставьте обновленную библиотеку DLL в локальную. `C:>.gacutil.exe /if .MFAAdapter.dll`

### <a name="view-assembly-in-the-gac-cmd-line"></a>Просмотреть сборку в GAC (Командная строка)

`C:> .gacutil.exe /l mfaadapter`

### <a name="register-your-provider-in-ad-fs"></a>Регистрация поставщика в AD FS

1. `PS C:>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.1, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

2. `PS C:>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter1”`

3. Перезагрузите службу AD FS.

### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>Создание политики проверки подлинности с помощью оснастки "Управление AD FS"

1. Откройте оснастку "Управление AD FS" (в меню " **Сервис** " Диспетчер сервера).

2. Щелкните **политики проверки подлинности**.

3. В разделе **многофакторная проверка подлинности**щелкните ссылку **изменить** справа от параметра **глобальные параметры**.

4. В разделе **Выбор дополнительных методов проверки подлинности**установите флажок для админнаме поставщика. Щелкните **Применить**.

5. Чтобы предоставить "триггер" для вызова MFA с помощью адаптера, в разделе расположения проверьте как **экстрасеть** , так и **интрасеть**, например. Щелкните **ОК**.

### <a name="authenticate-with-mfa-using-your-adapter"></a>Проверка подлинности с помощью MFA с использованием адаптера

Наконец, выполните следующие действия, чтобы проверить адаптер:

1. Убедитесь, что AD FS глобальный первичный тип проверки подлинности настроен как **Проверка подлинности с помощью форм** для экстрасети и интрасети (это упрощает проверку подлинности в качестве конкретного пользователя).

    1. В оснастке управления AD FS в разделе **политики проверки подлинности**в области **Основная проверка подлинности** щелкните **изменить** рядом с **параметром глобальные параметры**.

        1. Или просто перейдите на вкладку **Основная** в пользовательском интерфейсе многофакторной политики.

2. **Проверка подлинности** с помощью форм — единственный параметр, проверяемый как для **экстрасети** , так и для метода аутентификации в **интрасети** . Щелкните **ОК**.

3. Откройте HTML-страницу IDP инициировал вход (https:// <fsname> /адфс/лс/idpinitiatedsignon.htm) и выполните вход в качестве допустимого пользователя AD в тестовой среде.

4. Введите учетные данные для основной проверки подлинности.

5. Отобразится страница форм MFA с примером текста запроса.

    1. Если настроено несколько адаптеров, вы увидите страницу выбора MFA с понятным именем.

Вы должны увидеть успешный вход при вводе "адфабрик" на странице проверки подлинности MFA.

![Выполните вход с использованием адаптера](media/ad-fs-build-custom-auth-method/Dn783423.630d8a91-3bfe-4cba-8acf-03eae21530ee(MSDN.10).jpg "Выполните вход с использованием адаптера")

![Выполните вход с использованием адаптера](media/ad-fs-build-custom-auth-method/Dn783423.c340fa73-f70f-4870-b8dd-07900fea4469(MSDN.10).jpg "Выполните вход с использованием адаптера")

## <a name="see-also"></a>См. также

#### <a name="other-resources"></a>Другие ресурсы

[Дополнительные методы](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11)) 
 проверки подлинности [Управление рисками с помощью дополнительной многофакторной проверки подлинности для конфиденциальных приложений](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))
