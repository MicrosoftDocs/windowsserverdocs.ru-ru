---
title: 'Windows Admin Center: общие действия по устранению неполадок'
description: 'Windows Admin Center: общие действия по устранению неполадок (проект Honolulu)'
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.date: 01/15/2021
ms.openlocfilehash: d057a15b54ebabb6ed5e89dab7159aa1fa26c58d
ms.sourcegitcommit: 58a13a29869b39b6a6ba0db4d7b9fe1ff8371ea7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/21/2021
ms.locfileid: "98625817"
---
# <a name="troubleshooting-windows-admin-center"></a>Устранение неполадок в Windows Admin Center

> Область применения: центр администрирования Windows, Windows Admin Center, Azure Stack ХЦИ, версия v20H2

> [!Important]
> Это руководство поможет вам в диагностике и разрешении проблем, которые не позволяют использовать Windows Admin Center. Если у вас возникает проблема с определенным средством, проверьте, возможно, эта проблема [уже известна.](./known-issues.md)

## <a name="installer-fails-with-message-_the-module-microsoftpowershelllocalaccounts-could-not-be-loaded_"></a>Программа установки завершает работу с сообщением: **_не удалось загрузить модуль Microsoft. PowerShell. LocalAccounts._**

Это может произойти, если путь модуля PowerShell по умолчанию был изменен или удален. Чтобы устранить эту проблему, убедитесь, что ```%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules``` это **первый** элемент в переменной среды PSModulePath. Это можно сделать с помощью следующей строки PowerShell:

```powershell
[Environment]::SetEnvironmentVariable("PSModulePath","%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules;" + ([Environment]::GetEnvironmentVariable("PSModulePath","User")),"User")
```

## <a name="i-get-a-this-sitepage-cant-be-reached-error-in-my-web-browser"></a>В браузере появляется сообщение об ошибке **Не удается подключиться к этому сайту/странице**

### <a name="if-youve-installed-windows-admin-center-as-an-app-on-windows-10"></a>Если вы установили Windows Admin Center в качестве **приложения в Windows 10**

* Убедитесь, что Windows Admin Center запущен. Найдите элемент центр администрирования Windows значок центра администрирования Windows ![ ](../media/trayIcon.PNG) в области уведомлений или **Desktop/SmeDesktop.exeцентра администрирования Windows** в диспетчере задач. Если ни того, ни другого нет, запустите **Windows Admin Center** из меню "Пуск".

> [!NOTE]
> После перезагрузки необходимо запустить Windows Admin Center из меню "Пуск".

* [Проверьте версию Windows](#check-the-windows-version)

* Убедитесь, что вы используете браузер Microsoft Edge или Google Chrome.

* Вы выбрали правильный сертификат при [первом запуске?](../use/get-started.md#selecting-a-client-certificate)

  * Попробуйте открыть браузер в приватном режиме, и если это сработает, вам потребуется очистить кэш.

* Вы недавно выполнили обновление Windows 10 до новой сборки или версии?

  * Возможно, были удалены параметры доверенных узлов. [Выполните эти инструкции, чтобы обновить параметры доверенных узлов.](#configure-trustedhosts)

### <a name="if-youve-installed-windows-admin-center-as-a-gateway-on-windows-server"></a>Если вы установили Windows Admin Center в качестве **шлюза в Windows Server**

* [Проверьте версию Windows](#check-the-windows-version) на клиенте и сервере.

* Убедитесь, что вы используете браузер Microsoft Edge или Google Chrome.

* На сервере откройте диспетчер задач > службы и убедитесь, что **серверманажементгатевай/Windows Admin Center** работает.

    ![Диспетчер задач — вкладка «службы»](../media/Service-TaskMan.PNG)

* Проверьте сетевое подключение к шлюзу (замените на \<values> данные из развертывания).

    ```powershell
    Test-NetConnection -Port <port> -ComputerName <gateway> -InformationLevel Detailed
    ```

### <a name="if-you-have-installed-windows-admin-center-in-an-azure-windows-server-vm"></a>Если вы установили центр администрирования Windows на виртуальной машине Azure Windows Server,

* [Проверьте версию Windows](#check-the-windows-version)
* Добавили ли вы правило для портов входящего трафика HTTPS?
* [Дополнительные сведения об установке Windows Admin Center на виртуальной машине Azure](../azure/azure-integration.md)

### <a name="check-the-windows-version"></a>Проверьте версию Windows

* Откройте диалоговое окно "Выполнить" (клавиши Windows + R) и запустите ```winver```.

* Если вы используете Windows 10 версии 1703 или ниже, Windows Admin Center не поддерживается в вашей версии Microsoft Edge. Выполните обновление до более новой версии Windows 10, либо используйте Google Chrome.

* Если вы используете предварительную версию Windows 10 или сервера с версией сборки от 17134 до 17637, в Windows возникала ошибка, приведшая к сбою центра администрирования Windows. Используйте текущую поддерживаемую версию Windows.

### <a name="make-sure-the-windows-remote-management-winrm-service-is-running-on-both-the-gateway-machine-and-managed-node"></a>Убедитесь, что служба служба удаленного управления Windows (WinRM) запущена как на компьютере шлюза, так и на управляемом узле.

* Открытие диалогового окна запуска с помощью Виндовскэй + R
* Введите ```services.msc``` и нажмите клавишу ВВОД
* В открывшемся окне найдите служба удаленного управления Windows (WinRM), убедитесь, что он запущен и настроен на автоматический запуск.

### <a name="if-youre-getting-winrm-error-messages-while-managing-servers-in-windows-admin-center"></a>При получении сообщений об ошибках WinRM при управлении серверами в центре администрирования Windows

По умолчанию WinRM не разрешает делегирование учетных данных. Чтобы разрешить делегирование, на компьютере должен быть временно включен поставщик поддержки безопасности учетных данных (CredSSP).

Если вы получаете сообщения об ошибках WinRM, попробуйте воспользоваться инструкциями по проверке в разделе [Устранение неполадок вручную](https://docs.microsoft.com/azure-stack/hci/manage/troubleshoot-credssp#manual-troubleshooting) статьи [Устранение неполадок CredSSP](https://docs.microsoft.com/azure-stack/hci/manage/troubleshoot-credssp) для их устранения.

### <a name="did-you-upgrade-your-server-from-2016-to-2019"></a>Вы выполнили обновление сервера с 2016 до 2019?

* Возможно, были удалены параметры доверенных узлов. [Выполните эти инструкции, чтобы обновить параметры доверенных узлов.](#configure-trustedhosts)

## <a name="i-get-the-message-cant-connect-securely-to-this-page-this-might-be-because-the-site-uses-outdated-or-unsafe-tls-security-settings"></a>Я получаю сообщение: "не удается безопасно подключиться к этой странице. Это может быть вызвано тем, что сайт использует устаревшие или ненадежные параметры безопасности TLS.

Ваш компьютер ограничен подключениями HTTP/2. Центр администрирования Windows использует встроенную проверку подлинности Windows, которая не поддерживается в HTTP/2. Добавьте следующие два значения реестра в ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Http\Parameters``` ключ на компьютере, на **котором выполняется браузер** , чтобы удалить ограничение HTTP/2:

```
EnableHttp2Cleartext=dword:00000000
EnableHttp2Tls=dword:00000000
```

## <a name="im-having-trouble-with-the-remote-desktop-events-and-powershell-tools"></a>У меня возникли проблемы с удаленный рабочий стол, событиями и средствами PowerShell.

Для этих трех средств требуется протокол WebSocket, который обычно блокируется прокси-серверами и брандмауэрами. Если вы используете Google Chrome, существует [известная ошибка](known-issues.md#google-chrome) с WebSockets и проверкой подлинности NTLM.

## <a name="i-can-connect-to-some-servers-but-not-others"></a>Удается подключиться к некоторым серверам, но к другим нет

* Войдите на компьютер шлюза локально и попробуйте ```Enter-PSSession <machine name>``` в PowerShell, заменив \<machine name> именем компьютера, которым вы пытаетесь управлять, в центре администрирования Windows.

* Если в вашей среде вместо домена используется рабочая группа, см. [использование Windows Admin Center в рабочей группе](#using-windows-admin-center-in-a-workgroup).

* **Использование локальных учетных записей администратора.** При использовании учетной записи локального пользователя, которая не является встроенной учетной записью администратора, необходимо включить политику на целевом компьютере, выполнив следующую команду в PowerShell или в командной строке от имени администратора на целевом компьютере:

    ```
    REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
    ```

## <a name="using-windows-admin-center-in-a-workgroup"></a>Использование Windows Admin Center в рабочей группе

### <a name="what-account-are-you-using"></a>Какая учетная запись используется?
Убедитесь, что учетная запись, которую вы используете, входит в группу локальных администраторов на целевом сервере. В некоторых случаях WinRM также требует членство в группе "Пользователи удаленного управления". При использовании учетной записи локального пользователя, которая не является **встроенной учетной записью администратора**, необходимо включить политику на целевом компьютере, выполнив следующую команду в PowerShell или в командной строке от имени администратора на целевом компьютере:

```cmd
REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
```
### <a name="are-you-connecting-to-a-workgroup-machine-on-a-different-subnet"></a>Подключаетесь ли вы к компьютеру рабочей группы в другой подсети?

Для подключения к компьютеру рабочей группы, который находится не в одной подсети с шлюзом, убедитесь, что порт брандмауэра для WinRM (TCP 5985) пропускает входящий трафик на целевой компьютер. Вы можете выполнить следующую команду в PowerShell или в командной строке от имени администратора на целевом компьютере для создания этого правила брандмауэра:

- **Windows Server**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any
    ```

- **Windows 10**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any
    ```

### <a name="configure-trustedhosts"></a>Настройка TrustedHosts

При установке Windows Admin Center пользователю предоставляется возможность задать параметр TrustedHosts шлюза через Windows Admin Center. Это обязательно в среде рабочей группы и при использовании учетных данных локального администратора в домене. Если вы решили пропустить настройку этого параметра, необходимо вручную настроить TrustedHosts.

**Изменение TrustedHosts с помощью команд PowerShell:**

1. Откройте сеанс PowerShell от имени администратора.
2. Просмотрите текущие настройки TrustedHosts:

    ```powershell
    Get-Item WSMan:\localhost\Client\TrustedHosts
    ```

   > [!WARNING]
   > Если текущий параметр TrustedHosts не является пустым, приведенные ниже команды перезапишут его. Рекомендуется сохранить текущий параметр в текстовый файл с помощью следующей команды, чтобы его можно было восстановить при необходимости.
   >
   > `Get-Item WSMan:localhost\Client\TrustedHosts | Out-File C:\OldTrustedHosts.txt`

3. Задайте для TrustedHosts значение NetBIOS, IP-адреса или полного доменного имени компьютеров, которыми вы планируете управлять:

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '192.168.1.1,server01.contoso.com,server02'
    ```

   > [!TIP]
   > Простой способ задать все значения TrustedHosts за один раз заключается в использовании подстановочных знаков.
   >
   > ```powershell
   > Set-Item WSMan:\localhost\Client\TrustedHosts -Value '*'
   > ```

4. После завершения тестирования можно выполнить следующую команду в сеансе PowerShell с повышенными привилегиями для очистки параметров TrustedHosts:

    ```powershell
    Clear-Item WSMan:localhost\Client\TrustedHosts
    ```

5. Если вы ранее экспортировали параметры, откройте файл, скопируйте значения и используйте следующую команду:

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '<paste values from text file>'
    ```

## <a name="i-previously-had-windows-admin-center-installed-and-now-nothing-else-can-use-the-same-tcpip-port"></a>У меня был установлен центр администрирования Windows, и теперь никто не может использовать один и тот же порт TCP/IP.

Вручную выполните эти две команды в командной строке с повышенными привилегиями:

```cmd
netsh http delete sslcert ipport=0.0.0.0:443
netsh http delete urlacl url=https://+:443/
```

## <a name="azure-features-dont-work-properly-in-edge"></a>Функции Azure не работают должным образом на границе

На границе есть [Известные проблемы](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Known-issues-on-Edge) , связанные с зонами безопасности, которые влияют на вход Azure в центре администрирования Windows. Если у вас возникли проблемы с использованием функций Azure при использовании ребра, попробуйте добавить https://login.microsoftonline.com https://login.live.com и URL-адрес шлюза в качестве доверенных сайтов и дочерние сайты для параметров блокирования всплывающих окон в браузере на стороне клиента.

Выполните указанные ниже действия.
1. Поиск **свойств Интернета** в меню "Пуск" Windows
2. Перейдите на вкладку **Безопасность** .
3. В разделе **Доверенные сайты** нажмите кнопку **Сайты** и в открытом диалоговом окне добавьте нужные URL-адреса. Вам потребуется добавить URL-адрес шлюза, а также https://login.microsoftonline.com и https://login.live.com .
4. Перейдите на вкладку " **Конфиденциальность** "
5. В разделе **блокирование всплывающих окон** нажмите кнопку **Параметры** и добавьте URL-адреса в открывшемся диалоговом окне. Вам потребуется добавить URL-адрес шлюза, а также https://login.microsoftonline.com и https://login.live.com .

## <a name="having-an-issue-with-an-azure-related-feature"></a>Возникли проблемы с функцией, связанной с Azure?

Отправьте нам сообщение по электронной почте wacFeedbackAzure@microsoft.com со следующими сведениями:
* Общие сведения о проблемах из [перечисленных ниже вопросов](#providing-feedback-on-issues).
* Опишите вопрос и действия, которые были выполнены для воспроизведения проблемы.
* Вы ранее зарегистрировали шлюз в Azure с помощью New-AadApp.ps1 загружаемого скрипта, а затем выполнили обновление до версии 1807? Или вы зарегистрировали шлюз в Azure с помощью пользовательского интерфейса из параметров шлюза > Azure?
* Связана ли ваша учетная запись Azure с несколькими каталогами или клиентами?
    * Если да: при регистрации приложения Azure AD в центре администрирования Windows был использован каталог, используемый по умолчанию в Azure?
* Имеет ли ваша учетная запись Azure доступ к нескольким подпискам?
* Присоединена ли к подписке выставление счетов?
* Вошли ли вы в несколько учетных записей Azure, когда столкнулись с проблемой?
* Нужна ли учетная запись Azure для многофакторной проверки подлинности?
* Вы пытаетесь управлять виртуальной машиной Azure?
* Установлен ли центр администрирования Windows на виртуальной машине Azure?

## <a name="providing-feedback-on-issues"></a>Предоставление отзыва о проблемах

Перейдите в средство "Просмотр событий" > "Приложения и службы" > Microsoft-ServerManagementExperience и проверьте наличие каких-либо ошибок и предупреждений.

Отправьте сообщение об ошибке в разделе [UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5BBug%5D) с описанием проблемы.

Укажите все ошибки и предупреждения, которые удастся найти в журнале событий, а также следующие сведения:

* Платформа, на которой **установлен** Windows Admin Center (Windows 10 или Windows Server):
    * Если на сервере установлен, что такое [версия](#check-the-windows-version) Windows на компьютере, на **котором работает браузер** , для доступа к центру администрирования Windows:
    * Вы используете самозаверяющий сертификат, созданный установщиком?
    * Если вы используете свой собственный сертификат, соответствует ли имя субъекта компьютеру?
    * Если вы используете свой собственный сертификат, указано ли в нем альтернативное имя субъекта?
* Выполнена ли установка с настройками порта по умолчанию?
    * В противном случае, какой порт был указан?
* Компьютер, где **установлен** Windows Admin Center, присоединен к домену?
* [Версия](#check-the-windows-version) Windows, где **установлен** Windows Admin Center:
* Присоединен ли компьютер, который вы **пытаетесь отладить**, к домену?
* [Версия](#check-the-windows-version) Windows AC на компьютере, который вы **пытаетесь отладить**:
* Какой браузер вы используете?
    * Если вы используете Google Chrome, какая у него версия? (Справка > О Google Chrome)