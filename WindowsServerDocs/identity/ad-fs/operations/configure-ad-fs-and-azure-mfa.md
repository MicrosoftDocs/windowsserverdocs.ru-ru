---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: Настройка AD FS 2016 и Azure MFA
description: 'Подробнее: Настройка Azure MFA в качестве поставщика проверки подлинности с помощью AD FS'
ms.author: billmath
author: billmath
manager: mtillman
ms.date: 01/28/2019
ms.topic: article
ms.openlocfilehash: 8adcd7c06e769f2c457afde4faabdd4a3ca5e3c0
ms.sourcegitcommit: 6717decb5839aa340c81811d6fde020aabaddb3b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98781833"
---
# <a name="configure-azure-mfa-as-authentication-provider-with-ad-fs"></a>Настройка Azure MFA в качестве поставщика проверки подлинности с помощью AD FS

Если ваша организация состоит в федерации с Azure AD, вы можете использовать Многофакторную идентификацию Azure для защиты ресурсов AD FS как локально, так и в облаке. Azure MFA позволяет устранять пароли и обеспечивать более безопасный способ проверки подлинности.  Начиная с Windows Server 2016, теперь можно настроить Azure MFA для первичной проверки подлинности или использовать ее в качестве дополнительного поставщика проверки подлинности.

В отличие от AD FS в Windows Server 2012 R2, адаптер Azure MFA для AD FS 2016 интегрируется непосредственно с Azure AD и не требует локального сервера Azure MFA.   Адаптер Azure MFA встроен в Windows Server 2016, и нет необходимости в дополнительной установке.


## <a name="registering-users-for-azure-mfa-with-ad-fs"></a>Регистрация пользователей для Azure MFA с помощью AD FS

AD FS не поддерживает встроенную проверку &#34;&#34; или регистрацию сведений о проверке безопасности Azure MFA, таких как номер телефона или мобильное приложение. Это означает, что [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx) прежде чем использовать Azure MFA для проверки подлинности в AD FSных приложениях, пользователи должны пройти проверку.
Если пользователь, который еще не выполнил проверку подлинности в Azure AD, пытается пройти аутентификацию в Azure MFA на AD FS, он получит AD FS ошибку.  Как администратор AD FS вы можете настроить этот интерфейс с ошибками, чтобы указать пользователю страницу подтверждения вверху.  Это можно сделать с помощью onload.js настройки, чтобы определить строку сообщения об ошибке на странице AD FS и отобразить новое сообщение, чтобы пользователи могли посетить [https://aka.ms/mfasetup](https://aka.ms/mfasetup) , а затем повторить попытку проверки подлинности. Подробные инструкции см. в разделе "Настройка веб-страницы AD FS, чтобы помочь пользователям зарегистрировать методы проверки подлинности MFA" ниже в этой статье.

>[!NOTE]
> Ранее пользователям требовалось пройти проверку подлинности с помощью MFA для регистрации ( [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx) например, с помощью ярлыка [https://aka.ms/mfasetup](https://aka.ms/mfasetup) ).  Теперь AD FS пользователь, который еще не зарегистрировал сведения об аутентификации MFA, может получить доступ к странице Azure AD&#34;подтверждения вверху с помощью ярлыка, [https://aka.ms/mfasetup](https://aka.ms/mfasetup) используя только первичную проверку подлинности (например, встроенную проверку подлинности Windows или имя пользователя и пароль через веб-страницы AD FS).  Если у пользователя нет настроенных методов проверки, Azure AD будет выполнять встроенную регистрацию, в которой пользователь видит сообщение, &#34;администратору требуется настроить эту учетную запись для дополнительной проверки безопасности&#34;, и пользователь сможет &#34;настроить его&#34;.
> Пользователям, у которых уже настроен по крайней мере один метод проверки MFA, по-прежнему будет предложено предоставить MFA при посещении страницы подтверждения вверху.

## <a name="recommended-deployment-topologies"></a>Рекомендуемые топологии развертывания

### <a name="azure-mfa-as-primary-authentication"></a>Azure MFA в качестве основной проверки подлинности

Существует несколько замечательных причин использования Azure MFA в качестве основной проверки подлинности с помощью AD FS:

 - Чтобы избежать паролей для входа в Azure AD, Office 365 и других AD FS приложений
 - Чтобы защитить вход на основе пароля, требуется дополнительный фактор, например код проверки перед паролем.

Если вы хотите использовать Azure MFA в качестве основного метода проверки подлинности в AD FS для достижения этих преимуществ, вам, вероятно, потребуется также обеспечить возможность использования условного доступа Azure AD, включая &#34;true MFA&#34;, запрашивая дополнительные факторы в AD FS.

Теперь это можно сделать, настроив параметр домена Azure AD для локального задания MFA (установите &#34;SupportsMfa&#34; на $True).  В этой конфигурации AD FS может запросить Azure AD выполнить дополнительную проверку подлинности или &#34;true MFA&#34; для сценариев условного доступа, которым он необходим.

Как описано выше, любой пользователь AD FS, который еще не зарегистрировался (настроенные сведения о проверке MFA), должен получить запрос на странице настраиваемой AD FS страницы ошибок, чтобы перейти [https://aka.ms/mfasetup](https://aka.ms/mfasetup) к настройке сведений о проверке, а затем повторить попытку AD FS входа.
Поскольку Azure MFA в качестве первичного фактора считается одним фактором, после первоначальной настройки пользователям необходимо предоставить дополнительный фактор для управления сведениями об их проверке в Azure AD или для доступа к другим ресурсам, требующим MFA.

>[!NOTE]
> В ADFS 2019 необходимо внести изменения в тип утверждения привязки для Active Directory отношения доверия поставщика утверждений и изменить его с виндовсаккаунтнаме на UPN. Выполните командлет PowerShell, приведенный ниже. Это не влияет на внутреннюю работу AD FS фермы. Вы можете заметить, что при внесении этих изменений несколько пользователей могут повторно запрашивать учетные данные. После входа в систему конечные пользователи не увидят никаких различий.

```powershell
Set-AdfsClaimsProviderTrust -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -TargetName "Active Directory"
```

### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>Azure MFA в качестве дополнительной проверки подлинности для Office 365

Ранее, если вы хотели использовать Azure MFA в качестве дополнительного метода проверки подлинности в AD FS для Office 365 или других проверяющих сторон, лучшим вариантом было Настройка Azure AD для выполнения составного многофакторного MFA, в котором основная проверка подлинности выполняется в локальной среде AD FS и MFA активируется Azure AD.
Теперь можно использовать Azure MFA в качестве дополнительной проверки подлинности в AD FS если параметру Domain SupportsMfa присвоено значение $True.

Как описано выше, любой пользователь AD FS, который еще не зарегистрировался (настроенные сведения о проверке MFA), должен получить запрос на странице настраиваемой AD FS страницы ошибок, чтобы перейти [https://aka.ms/mfasetup](https://aka.ms/mfasetup) к настройке сведений о проверке, а затем повторить попытку AD FS входа.

## <a name="pre-requisites"></a>Предварительные требования

Следующие предварительные требования необходимы при использовании Azure MFA для проверки подлинности с AD FS.

- [Подписка Azure с Azure Active Directory](https://azure.microsoft.com/pricing/free-trial/).
- [Многофакторная идентификация Azure](/azure/active-directory/authentication/concept-mfa-howitworks)


> [!NOTE]
> Azure AD и Azure MFA включены в Azure AD Premium и Enterprise Mobility Suite (EMS).  Если у вас есть один из этих элементов, отдельные подписки не требуются.

- Локальная среда Windows Server 2016 AD FS.
   - Сервер должен иметь возможность взаимодействия со следующими URL-адресами через порт 443.
      - https://adnotifications.windowsazure.com
      - https://login.microsoftonline.com
- Локальная среда является [Федеративной с Azure AD.](/azure/active-directory/hybrid/how-to-connect-install-custom#configuring-federation-with-ad-fs)
- [Модуль windows Azure Active Directory для Windows PowerShell](/powershell/module/azuread/).
- Разрешения глобального администратора в экземпляре Azure AD, чтобы настроить его с помощью Azure AD PowerShell.
- Учетные данные администратора предприятия для настройки фермы AD FS для Azure MFA.

## <a name="configure-the-ad-fs-servers"></a>Настройка серверов AD FS

Чтобы завершить настройку Azure MFA для AD FS, необходимо настроить каждый сервер AD FS, выполнив описанные действия.

>[!NOTE]
>Убедитесь, что эти действия выполняются на **всех** серверах AD FS фермы. Если в ферме имеется несколько AD FS серверов, можно выполнить необходимую настройку удаленно с помощью Azure AD PowerShell.

### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>Шаг 1. Создание сертификата для Azure MFA на каждом AD FS сервере с помощью `New-AdfsAzureMfaTenantCertificate` командлета

Первое, что нужно сделать, — это создать сертификат для использования Azure MFA.  Это можно сделать с помощью PowerShell.  Созданный сертификат можно найти в хранилище сертификатов "локальные компьютеры", и оно помечено именем субъекта, содержащим ИД клиента для каталога Azure AD.

![Снимок экрана хранилища сертификатов на локальном компьютере, на котором показан созданный сертификат.](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)

Обратите внимание, что TenantID — это имя каталога в Azure AD.  Используйте следующий командлет PowerShell для создания нового сертификата.
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`

![Снимок экрана окна PowerShell, отображающего приведенный выше командлет.](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)

### <a name="step-2-add-the-new-credentials-to-the-azure-multi-factor-auth-client-service-principal"></a>Шаг 2. Добавление новых учетных данных в субъект-службу клиента многофакторной проверки подлинности Azure

Чтобы серверы AD FS могли взаимодействовать с клиентом многофакторной идентификации Azure, необходимо добавить учетные данные субъекта-службы для клиента многофакторной проверки подлинности Azure. Сертификаты, созданные с помощью `New-AdfsAzureMFaTenantCertificate` командлета, будут использоваться в качестве этих учетных данных. Выполните следующие действия с помощью PowerShell, чтобы добавить новые учетные данные в субъект-службу клиента многофакторной проверки подлинности Azure.

> [!NOTE]
> Чтобы выполнить этот шаг, необходимо подключиться к экземпляру Azure AD с помощью PowerShell, используя `Connect-MsolService` .  В этих шагах предполагается, что вы уже подключены через PowerShell.  Дополнительные сведения см [ `Connect-MsolService` .](/previous-versions/azure/dn194123(v=azure.100)) в разделе.

**Настройка сертификата в качестве новых учетных данных для клиента многофакторной идентификации Azure**

`New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64`

> [!IMPORTANT]
> Эту команду необходимо выполнить на всех AD FS серверах в ферме.  Azure AD MFA завершится сбоем на серверах, на которых не установлен сертификат в качестве новых учетных данных для клиента многофакторной идентификации Azure.

> [!NOTE]
> 981f26a1-7f43-403b-a875-f8b09b8cd720 — это идентификатор GUID для клиента многофакторной идентификации Azure.

## <a name="configure-the-ad-fs-farm"></a>Настройка фермы AD FS

Завершив работу с предыдущим разделом на каждом AD FS сервере, настройте сведения о клиенте Azure с помощью командлета [Set-адфсазуремфатенант](/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata) . Этот командлет необходимо выполнить только один раз для фермы AD FS.

Откройте командную строку PowerShell и введите свой идентификатор *tenantId* с помощью командлета [Set-адфсазуремфатенант](/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata) . Для клиентов, использующих Microsoft Azure для государственных организаций Cloud, добавьте `-Environment USGov` параметр:

> [!NOTE]
> Прежде чем эти изменения вступят в силу, необходимо перезапустить службу AD FS на каждом сервере в ферме. Для минимального воздействия переведите каждый AD FSный сервер из вращения балансировки сетевой нагрузки по одному за раз и дождитесь завершения всех соединений.

```powershell
Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720
```

![Снимок экрана окна PowerShell, отображающего предупреждающее сообщение, полученное после выполнения командлета Set-AdfsAzureMfaTenant.](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)

Windows Server без последнего пакета обновления не поддерживает `-Environment` параметр командлета [Set-адфсазуремфатенант](/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata) . Если вы используете облако Azure для государственных организаций, и на предыдущих шагах не удалось настроить клиент Azure из-за отсутствующего `-Environment` параметра, выполните следующие действия, чтобы вручную создать записи реестра. Пропустите эти шаги, если предыдущий командлет правильно зарегистрировал сведения о клиенте или вы не в облаке Azure для государственных организаций:

1. Откройте **редактор реестра** на AD FS сервере.
1. Перейдите на страницу `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ADFS`. Создайте следующие значения разделов реестра:

    | Раздел реестра       | Значение |
    |--------------------|-----------------------------------|
    | SasUrl             | https://adnotifications.windowsazure.us/StrongAuthenticationService.svc/Connector |
    | стсурл             | https://login.microsoftonline.us |
    | ResourceUri        | https://adnotifications.windowsazure.us/StrongAuthenticationService.svc/Connector |

1. Прежде чем эти изменения вступят в силу, перезапустите службу AD FS на каждом сервере в ферме. Для минимального воздействия переведите каждый AD FSный сервер из вращения балансировки сетевой нагрузки по одному за раз и дождитесь завершения всех соединений.

После этого вы увидите, что Azure MFA доступен в качестве основного метода проверки подлинности для использования в интрасети и экстрасети.

![Снимок экрана диалогового окна "изменение методов проверки подлинности", в котором показан параметр Azure M F A, выделенный в разделах экстрасети и интрасети.](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA6.png)

## <a name="renew-and-manage-ad-fs-azure-mfa-certificates"></a>Продление AD FS сертификатов Azure MFA и управление ими

В следующих руководствах описано, как управлять сертификатами Azure MFA на серверах AD FS.
По умолчанию при настройке AD FS с помощью Azure MFA сертификаты, созданные с помощью `New-AdfsAzureMfaTenantCertificate` командлета PowerShell, действительны в течение 2 лет.  Чтобы определить, насколько близко истекает срок действия сертификатов, а затем продлить и установить новые сертификаты, выполните следующую процедуру.

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>Оценка даты истечения срока действия сертификата Azure MFA AD FS

На каждом AD FS сервере в моем хранилище локального компьютера будет существовать самозаверяющий сертификат с &#34;OU = Microsoft AD FS Azure MFA&#34; в поставщике и субъекте.  Это сертификат Azure MFA.  Проверьте срок действия этого сертификата на каждом сервере AD FS, чтобы определить дату истечения срока.

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>Создание нового AD FS сертификата Azure MFA на каждом сервере AD FS

Если срок действия сертификатов приближается к концу, запустите процесс продления, создав новый сертификат Azure MFA на каждом AD FS сервере. В командном окне PowerShell создайте новый сертификат на каждом AD FS сервере с помощью следующего командлета:

> [!CAUTION]
> Если срок действия сертификата уже истек, не добавляйте `-Renew $true` параметр в следующую команду. В этом случае существующий сертификат с истекшим сроком действия заменяется новым, а не оставляется на месте и создается дополнительный сертификат.

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

Если срок действия сертификата еще не истек, то создается новый сертификат, который действителен через 2 дня в будущем до 2 дней + 2 года. AD FS и операции Azure MFA не затрагиваются этим командлетом или новым сертификатом. (Примечание. задержка в 2 дня преднамерена и предоставляет время для выполнения приведенных ниже действий по настройке нового сертификата в клиенте перед тем, как AD FS начнет использовать его для Azure MFA.)

### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>Настройка каждого нового AD FS сертификата Azure MFA в клиенте Azure AD

С помощью модуля Azure AD PowerShell для каждого нового сертификата (на каждом AD FS сервере) обновите параметры клиента Azure AD следующим образом (Примечание. сначала необходимо подключиться к клиенту с помощью `Connect-MsolService` для выполнения следующих команд).

```
PS C:/> New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type Asymmetric -Usage Verify -Value $newcert
```

Если срок действия предыдущего сертификата уже истек, перезапустите службу AD FS, чтобы выбрать новый сертификат. Вам не нужно перезапускать службу AD FS, если вы обновили сертификат до истечения срока его действия.

### <a name="verify-that-the-new-certificates-will-be-used-for-azure-mfa"></a>Убедитесь, что для Azure MFA будут использоваться новые сертификаты.

После того, как новые сертификаты станут действительными, AD FS выберет их и начнет использовать каждый соответствующий сертификат для Azure MFA в течение нескольких часов в день.  После этого на каждом сервере появится событие, зарегистрированное в журнале событий администратора AD FS, со следующими сведениями:

```
Log Name:      AD FS/Admin
Source:        AD FS
Date:          2/27/2018 7:33:31 PM
Event ID:      547
Task Category: None
Level:         Information
Keywords:      AD FS
User:          DOMAIN\adfssvc
Computer:      ADFS.domain.contoso.com
Description:
The tenant certificate for Azure MFA has been renewed.

TenantId: contoso.onmicrosoft.com.
Old thumbprint: 7CC103D60967318A11D8C51C289EF85214D9FC63.
Old expiration date: 9/15/2019 9:43:17 PM.
New thumbprint: 8110D7415744C9D4D5A4A6309499F7B48B5F3CCF.
New expiration date: 2/27/2020 2:16:07 AM.
```

## <a name="customize-the-ad-fs-web-page-to-guide-users-to-register-mfa-verification-methods"></a>Настройка веб-страницы AD FS для указания пользователям регистрации методов проверки MFA

Используйте следующие примеры для настройки веб-страниц AD FS для пользователей, которые еще не выполнили проверку (настроенные сведения о проверке MFA).

### <a name="find-the-error"></a>Поиск ошибки

Во-первых, существует несколько различных сообщений об ошибках, AD FS будет возвращаться в случае, если у пользователя отсутствуют сведения для проверки.
Если в качестве основной проверки подлинности используется Azure MFA, непроверенный пользователь увидит AD FS страницу ошибки, содержащую следующие сообщения:
```
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            Authentication attempt failed. Select a different sign in option or close the web browser and sign in again. Contact your administrator for more information.
        </div>
```
При появлении попытки выполнить дополнительную проверку подлинности в Azure AD непроверенный пользователь увидит AD FS страницу ошибки, содержащую следующие сообщения:
```
<div id='mfaGreetingDescription' class='groupMargin'>For security reasons, we require additional information to verify your account (mahesh@jenfield.net)</div>
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            The selected authentication method is not available for &#39;username@contoso.com&#39;. Choose another authentication method or contact your system administrator for details.
        </div>
```

### <a name="catch-the-error-and-update-the-page-text"></a>Перехватить ошибку и обновить текст страницы

Чтобы перехватить ошибку и отобразить пользовательское руководство, просто добавьте JavaScript в конец файла onload.js, который является частью AD FS веб-темы.  Это позволяет выполнять следующие действия.
 - Поиск идентифицирующих строк ошибок
 - укажите пользовательское веб-содержимое.

> [!NOTE]
> Общие сведения о настройке файла onload.js см. в статье [Расширенная настройка AD FS страниц входа в](advanced-customization-of-ad-fs-sign-in-pages.md)систему.

Вот простой пример, который может потребоваться расширить:

1. Откройте Windows PowerShell на основном сервере AD FS и создайте новую веб-тему AD FS, выполнив следующую команду:

    ``` PowerShell
        New-AdfsWebTheme –Name ProofUp –SourceName default
    ```
2. Затем создайте папку и экспортируйте веб-тему AD FS по умолчанию:

    ``` PowerShell
       New-Item -Path 'c:\Theme' -ItemType Directory;Export-AdfsWebTheme –Name default –DirectoryPath c:\Theme
    ```
3. Открытие файла C:\Theme\script\onload.js в текстовом редакторе
4. Добавьте следующий код в конец файла onload.js

    ``` JavaScript
    //Custom Code
    //Customize MFA exception
    //Begin

    var domain_hint = "<YOUR_DOMAIN_NAME_HERE>";
    var mfaSecondFactorErr = "The selected authentication method is not available for";
    var mfaProofupMessage = "You will be automatically redirected in 5 seconds to set up your account for additional security verification. Once you have completed the setup, please return to the application you are attempting to access.<br><br>If you are not redirected automatically, please click <a href='{0}'>here</a>."
    var authArea = document.getElementById("authArea");
    if (authArea) {
        var errorMessage = document.getElementById("errorMessage");
        if (errorMessage) {
            if (errorMessage.innerHTML.indexOf(mfaSecondFactorErr) >= 0) {

                //Hide the error message
                var openingMessage = document.getElementById("openingMessage");
                if (openingMessage) {
                    openingMessage.style.display = 'none'
                }
                var errorDetailsLink = document.getElementById("errorDetailsLink");
                if (errorDetailsLink) {
                    errorDetailsLink.style.display = 'none'
                }

                //Provide a message and redirect to Azure AD MFA Registration Url
                var mfaRegisterUrl = "https://account.activedirectory.windowsazure.com/proofup.aspx?proofup=1&whr=" + domain_hint;
                errorMessage.innerHTML = "<br>" + mfaProofupMessage.replace("{0}", mfaRegisterUrl);
                window.setTimeout(function () { window.location.href = mfaRegisterUrl; }, 5000);
            }
        }
    }

    //End Customize MFA Exception
    //End Custom Code
    ```
    > [!IMPORTANT]
    > Необходимо изменить "<YOUR_DOMAIN_NAME_HERE>"; для использования доменного имени. Пример: `var domain_hint = "contoso.com";`

5. Сохранение файла onload.js
6. Импортируйте файл onload.js в пользовательскую тему, введя следующую команду Windows PowerShell:

    ``` PowerShell
    Set-AdfsWebTheme -TargetName ProofUp -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';path="c:\theme\script\onload.js"}
    ```
7. Наконец, примените пользовательскую веб-тему AD FS, введя следующую команду Windows PowerShell:

    ``` PowerShell
    Set-AdfsWebConfig -ActiveThemeName "ProofUp"
    ```

## <a name="next-steps"></a>Дальнейшие действия

[Управление протоколами TLS/SSL и комплектами шифров, используемыми AD FS и Azure MFA](manage-ssl-protocols-in-ad-fs.md)
