---
ms.assetid: 882abec8-0189-4f73-99c5-792987168080
title: Расширенная настройка страниц входа AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 01/16/2019
ms.topic: article
ms.openlocfilehash: 296d3e310818dcaee8443810b922ce6bf0389537
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97040262"
---
# <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>Расширенная настройка страниц входа AD FS


## <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>Расширенная настройка AD FS \- страниц входа
AD FS в Windows Server 2012 R2 предоставляет встроенную \- поддержку для настройки входа в систему \- . В большинстве этих сценариев \- все, что требуется, являются встроенными командлетами Windows PowerShell.  Рекомендуется использовать встроенные \- команды Windows PowerShell, чтобы настроить стандартные элементы для AD FS входа \- в систему везде, где это возможно.  Дополнительные сведения см. [в статье Настройка входа пользователя AD FS](AD-FS-user-sign-in-customization.md) .

В некоторых случаях AD FS администраторам может потребоваться предоставить дополнительные возможности входа \- , которые невозможно выполнить с помощью существующих команд PowerShell, поставляемых в комплекте \- с AD FS. В некоторых случаях можно использовать приведенные \( ниже инструкции \) для администраторов по настройке \- интерфейса входа, добавляя дополнительную логику к **onload.js** , предоставляемую AD FS и выполняемую на всех AD FS страницах.

## <a name="things-to-know-before-you-start"></a>Вопросы, которые необходимо изучить перед началом работы

-   Любое изменение, влияющее на перенаправление потоков или изменение параметров протокола, которые AD FS работает с, не поддерживается.

-   Исходная onload.js, которая поставляется вместе с веб-темой по умолчанию, содержит код, обрабатывающий отрисовку страниц для различных конструктивных параметров. Рекомендуется не изменять содержимое исходного onload.js, но добавлять код в существующие onload.js, обрабатывающие пользовательскую логику.

-   AD FS поставляется с встроенной \- веб-темой, которая называется по умолчанию. Нельзя изменить onload.js веб-темы по умолчанию. Чтобы обновить onload.js, необходимо создать и использовать пользовательскую веб-тему для AD FS страниц входа \- .  Сведения о создании пользовательской веб-темы см. в статье [Настройка входа пользователя AD FS](AD-FS-user-sign-in-customization.md) .

-   Тот же onload.js будет выполняться на всех страницах ADFS, \( например \-страница входа на основе форм, страница обнаружения домашней области и т. д. \) Необходимо убедиться, что код в скрипте выполняется только в том виде, в котором он создан, и не будет выполняться непредвиденным образом.

-   При ссылке на любой HTML-элемент убедитесь, что всегда проверяется наличие элемента перед началом работы с элементом. Это обеспечивает надежность и гарантирует, что пользовательская логика не будет выполняться на страницах, не содержащих этот элемент. Можно просто просмотреть исходный код HTML на AD FS страницах входа, \- чтобы просмотреть существующие элементы.

-   Настоятельно рекомендуется проверить настройки в другой среде и протестировать их перед развертыванием на рабочих AD FS серверах. Это снижает вероятность предоставления конечным пользователям таких настроек до проверки.

## <a name="customizing-the-ad-fs-sign-in-experience-by-using-onloadjs"></a>Настройка интерфейса входа AD FS с \- помощью onload.js
При настройке onload.js для службы AD FS выполните следующие действия.

#### <a name="customizing-onloadjs-for-the-ad-fs-service"></a>Настройка onload.js для службы AD FS

1.  Чтобы добавить пользовательскую логику в onload.js, необходимо сначала создать пользовательскую веб-тему. Тема, которая поставляется \- из \- \- комплекта, называется по умолчанию. Можно экспортировать тему по умолчанию и воспользоваться ей, чтобы быстро приступить к работе. Следующий командлет создает пользовательскую веб-тему, которая дублирует веб-тему по умолчанию:

    ```
    New-AdfsWebTheme –Name custom –SourceName default

    ```

2.  Затем можно экспортировать пользовательскую или веб-тему по умолчанию, чтобы получить onload.js файл. Чтобы экспортировать веб-тему, используйте следующий командлет:

    ```
    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme

    ```

    Вы найдете onload.js в папке script в каталоге, указанном выше, и добавьте пользовательскую логику в скрипт, \( см. пример ниже в разделе варианты использования \) .

3.  Внесите необходимые изменения, чтобы настроить onload.js в соответствии с вашими нуждами.

4.  Обновите тему, используя измененные onload.js. Используйте следующий командлет, чтобы применить обновление onload.js к пользовательской веб-теме:

     Для AD FS в Windows Server 2012 R2:

    ```
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';path="c:\theme\script\onload.js"}

    ```
    Для AD FS в Windows Server 2016:

     ```
    Set-AdfsWebTheme -TargetName custom -OnLoadScriptPath "c:\theme\script\onload.js"

    ```

5.  Чтобы применить пользовательскую веб-тему к AD FS, используйте следующий командлет:

    ```
    Set-AdfsWebConfig -ActiveThemeName custom
    ```

## <a name="additional-customization-examples"></a>Дополнительные примеры настройки
Ниже приведены примеры пользовательского кода, добавленного в onload.js для различных целей тонкой \- настройки. При добавлении пользовательского кода всегда добавляйте пользовательский код в нижнюю часть onload.js.

### <a name="example-1-change-sign-in-with-organizational-account-string"></a>Пример 1. изменение "вход с использованием учетной записи организации"
По умолчанию на \- странице входа на основе формы AD FS \- заголовком "вход с учетной записью организации" над полями ввода пользователя.

Если вы хотите заменить эту строку собственной строкой, можно добавить следующий код для onload.js.

```
// Sample code to change "Sign in with organizational account" string.

// Check whether the loginMessage element is present on this page.
var loginMessage = document.getElementById('loginMessage');
if (loginMessage)
{
       // loginMessage element is present, modify its properties.
       loginMessage.innerHTML = 'Your company description text';
}

```

### <a name="example-2-accept-sam-account-name-as-a-login-format-on-an-ad-fs-form-based-sign-in-page"></a>Пример 2. принятие \- имени учетной записи SAM в качестве формата входа на AD FS на \- странице входа на основе формы \-
Страница входа по умолчанию AD FS форме \- \- поддерживает формат входа в систему имен субъектов-пользователей \( UPN \) \( , например, <strong>johndoe@contoso.com</strong> \) или доменных \- имен SAM учетных записей \( **contoso \\ JohnDoe** или **contoso.com \\ JohnDoe** \) . Если все пользователи поступают из одного и того же домена, и они только узнают об \- именах учетных записей SAM, может потребоваться поддержка сценария, в котором пользователи могут войти в систему, используя \- только имена учетных записей SAM. Вы можете добавить следующий код onload.js для поддержки этого сценария, просто замените домен "contoso.com" в примере ниже на домен, который вы хотите использовать.

```
if (typeof Login != 'undefined'){
    Login.submitLoginRequest = function () {
    var u = new InputUtil();
    var e = new LoginErrors();
    var userName = document.getElementById(Login.userNameInput);
    var password = document.getElementById(Login.passwordInput);
    if (userName.value && !userName.value.match('[@\\\\]'))
    {
        var userNameValue = 'contoso.com\\' + userName.value;
        document.forms['loginForm'].UserName.value = userNameValue;
    }

    if (!userName.value) {
       u.setError(userName, e.userNameFormatError);
       return false;
    }

    if (!password.value)
    {
        u.setError(password, e.passwordEmpty);
        return false;
    }
    document.forms['loginForm'].submit();
    return false;
};
}

```

## <a name="additional-references"></a>Дополнительная справка
[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)


