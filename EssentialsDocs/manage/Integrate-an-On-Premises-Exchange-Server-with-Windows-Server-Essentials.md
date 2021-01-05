---
title: Интеграция локального сервера Exchange Server с Windows Server Essentials
description: Узнайте, как настроить и интегрировать локальный сервер, на котором работает Exchange Server, с сервером под управлением Windows Server Essentials.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: b56a21e2-c9e3-4ba9-97d9-719ea6a0854b
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: aef1d55d3743dcee483b4e6e9e1cca5ae33682e9
ms.sourcegitcommit: e00e789dff216dbade861e61365f078b758a5720
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2020
ms.locfileid: "97755330"
---
# <a name="integrate-an-on-premises-exchange-server-with-windows-server-essentials"></a>Интеграция локального сервера Exchange Server с Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Данное руководство содержит сведения и основные инструкции по настройке и интеграции локального сервера, работающего под управлением Exchange Server, с сервером под управлением Windows Server Essentials.

 Рекомендуется ознакомиться с этим руководством, прежде чем приступать к развертыванию локального сервера Exchange Server в сети Windows Server Essentials.

> [!NOTE]
>  Exchange Server 2010 не поддерживает установку на компьютерах под управлением Windows Server 2012.

## <a name="prerequisites"></a>Предварительные требования
 Прежде чем установить сервер Exchange Server в сети Windows Server Essentials, необходимо выполнить следующие действия.

-   [Настройка сервера, работающего под управлением Windows Server Essentials](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SetUpSBS8)

-   [Подготовка второго сервера, где будет установлен Exchange Server](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SecondServer)

-   [Настройка имени домена Интернета](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_DomainNames)

###  <a name="set-up-a-server-that-is-running-windows-server-essentials"></a><a name="BKMK_SetUpSBS8"></a> Настройка сервера под Windows Server Essentials
 Сервер Windows Server Essentials должен быть настроен заранее. Он будет выполнять роль контроллера домена для сервера Exchange Server. Сведения о настройке Windows Server Essentials, см. в разделе [Установка Windows Server Essentials](../install/Install-Windows-Server-Essentials.md).

###  <a name="prepare-a-second-server-on-which-to-install-exchange-server"></a><a name="BKMK_SecondServer"></a> Подготовка второго сервера для установки Exchange Server
 Необходимо установить Exchange Server на втором сервере, работающем под управлением версии Windows Server, официально поддерживающей Exchange Server 2010 или Exchange Server 2013. Затем нужно присоединить второй сервер к домену Windows Server Essentials.

 Сведения о том, как присоединить второй сервер к домену Windows Server Essentials, см. в разделе Подключение второго сервера к сети в [подсоединении](../use/Get-Connected-in-Windows-Server-Essentials.md).

> [!NOTE]
>  Майкрософт не поддерживает установку Exchange Server на сервере, работающем под управлением Windows Server Essentials.

###  <a name="configure-your-internet-domain-name"></a><a name="BKMK_DomainNames"></a> Настройка доменного имени в Интернете
 Чтобы интегрировать локальный сервер Exchange Server с Windows Server Essentials, у вашей компании должно быть зарегистрированное действительное имя домена Интернета (например, *contoso.com*). Вы также должны совместно с поставщиком имени домена создать записи ресурсов DNS, необходимые для сервера Exchange Server.

 Например, если имя домена Интернета для вашей компании — contoso.com и вы хотите использовать полное доменное имя *mail.contoso.com* для ссылки на свой локальный сервер Exchange Server, вместе с поставщиком имени домена создайте записи ресурсов DNS в следующей таблице.


| Имя записи ресурса |     Тип записи     |                                                                         Параметры записи                                                                          |                                                                                                                                                                                                                                                              Описание                                                                                                                                                                                                                                                              |
|----------------------|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         mail         |      Узел (A)       |                                                        Address=*общий IP-адрес, назначенный поставщиком услуг Интернета*                                                         |                                                                                                                                                                                                   Сервер Exchange Server будет получать почту, адресованную на mail.contoso.com.<br /><br /> Можно использовать другое имя по своему выбору.                                                                                                                                                                                                    |
|          MX          | Почтовый обменник (MX) |                                            Hostname=@<br /><br /> Address=mail.contoso.com<br /><br /> Preference=0                                             |                                                                                                                                                                                                      Обеспечивает маршрутизацию сообщений электронной почты для email@contoso.com прибытия на локальный сервер, на котором работает Exchange Server.                                                                                                                                                                                                       |
|         SPF          |     Текст (TXT)      |                                                                        v=spf1 a mx ~all                                                                         |                                                                                                                                                                                                                      Запись ресурса, которая не позволяет идентифицировать как спам электронные сообщения, отправленные с вашего сервера.                                                                                                                                                                                                                      |
|  autodiscover._tcp   |    Служба (SRV)    | Service: _autodiscover<br /><br /> Protocol: _tcp<br /><br /> Priority: 0<br /><br /> Weight: 0<br /><br /> Port: 443<br /><br /> Target host: mail.contoso.com | Настраивает Microsoft Office Outlook и мобильные устройства на автоматическое обнаружение вашего локального сервера Exchange Server.<br /><br /> **Примечание.** Можно также настроить запись ресурса узла автообнаружения (A) и указать записи на общедоступный IP-адрес локального сервера, на котором работает Exchange Server. Однако в этом случае необходимо предоставить сертификат SSL для дополнительного имени субъекта, поддерживающий оба доменных имени — mail.contoso.com и autodiscover.contoso.com. |

> [!NOTE]
>  -   Замените вхождения *contoso.com* в этом примере именем домена Интернета, которое вы зарегистрировали.

 Вы должны выбрать полное доменное имя для вашего локального сервера Exchange Server, не совпадающее с полным доменным именем сервера Windows Server Essentials. Например, можно выбрать полное доменное имя *remote.contoso.com*, которое компьютеры будут использовать для доступа к серверу Windows Server Essentials из Интернета. Полное доменное имя *mail.contoso.com* можно использовать для перенаправления электронной почты на локальный сервер Exchange Server.

## <a name="install-exchange-server"></a>Установка сервера Exchange Server
 Функция интеграции Exchange Server в Windows Server Essentials поддерживает следующие версии Exchange Server:

- Exchange Server 2013;

- Exchange Server 2010 с пакетом обновления 1 (SP1)

  Прежде чем установить Exchange Server на втором сервере, нужно добавить учетную запись текущего администратора в группу **Enterprise Admins**.

#### <a name="to-add-the-current-administrator-account-to-the-enterprise-admins-group"></a>Добавление учетной записи текущего администратора в группу администраторов предприятия

1.  Войдите в Windows Server Essentials в качестве администратора.

2.  Запустите Windows PowerShell от имени администратора.

3.  В командной строке Windows PowerShell введите **Add-адграупмембер "корпоративные администраторы" $env: username**, а затем нажмите клавишу ВВОД.

#### <a name="to-install-exchange-server"></a>Установка сервера Exchange Server

1.  Войдите в систему второго сервера с правами администратора.

2.  Откройте браузер и перейдите на веб-сайт [помощника по развертыванию сервера Exchange Server](https://go.microsoft.com/fwlink/p/?LinkID=249163) .

3.  Щелкните **On-Premises Only** (Только локально).

4.  Выберите вариант новой установки для версии Exchange Server, которую вы собираетесь установить.

    > [!NOTE]
    >  В случае миграции с Windows Small Business Server следует выбрать подходящий вариант обновления, включающий процесс миграции.

5.  На следующей странице, не изменяя заданные по умолчанию значения, нажмите кнопку **Next** (Далее).

    > [!NOTE]
    >  Если вы планируете использовать общедоступные папки в новой установке Exchange Server, измените значение этого параметра на **Yes** (Да).

6.  Следуйте пошаговым инструкциям в контрольном списке для развертывания Exchange Server.

     Помощник по развертыванию сервера Exchange Server также позволяет вам:

    -   распечатать копию контрольного списка,

    -   отправить копию контрольного списка по электронной почте.

    -   загрузить контрольный список в виде PDF-файла.

> [!NOTE]
> - Всегда необходимо устанавливать средства управления на сервере Exchange Server. Средства управления необходимы для функции интеграции сервера Exchange Server в Windows Server Essentials.
>   -   Если вам нужно настроить виртуальные каталоги, рекомендуется также задать для свойства **InternalUrl** каждого виртуального каталога тот же URL-адрес, что и для свойства **ExternalUrl**. Дополнительную информацию см. в статье [Управление виртуальными каталогами сервера клиентского доступа](https://go.microsoft.com/fwlink/p/?LinkId=251058) на веб-сайте справки Exchange Server 2010.
>   -   Если вам требуется доступ к Outlook Web Access (OWA) с сайта удаленного веб-доступа в Windows Server Essentials, необходимо задать свойство External URL для OWA.

 В случае чистой установки Exchange Server 2010 можно также использовать следующие сценарии.

#### <a name="to-use-scripts-to-set-up-exchange-server"></a>Использование сценариев для установки Exchange Server

1.  Откройте Блокнот и вставьте следующий сценарий в новый файл:

```powershell
Import-Module ServerManager

Add-WindowsFeature NET-Framework,RSAT-ADDS,Web-Server,Web-Basic-Auth,Web-Windows-Auth,Web-Metabase,Web-Net-Ext,Web-Lgcy-Mgmt-Console,WAS-Process-Model,RSAT-Web-Server,Web-ISAPI-Ext,Web-Digest-Auth,Web-Dyn-Compression,NET-HTTP-Activation,Web-Asp-Net,Web-Client-Auth,Web-Dir-Browsing,Web-Http-Errors,Web-Http-Logging,Web-Http-Redirect,Web-Http-Tracing,Web-ISAPI-Filter,Web-Request-Monitor,Web-Static-Content,Web-WMI,RPC-Over-HTTP-Proxy  Restart
```

2. Сохраните файл как **InstallDependencies.ps1**.

3. Скопируйте сертификат SSL для Exchange в каталог на сервере.

4. Откройте новый файл Блокнота и скопируйте в него следующий текст:

```powershell
param (
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "The path to your Certificate file, must be a *.pfx format")]
    $CertPath = "c:\certificates\ExchangeCertificate.pfx",
    [Security.SecureString]
    [Parameter(Mandatory=$true, HelpMessage = "The password of your cert")]
    $CertPassword = $null,
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Domain Name, eg. contoso.com")]
    $DomainName = "contoso.com",
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Server IP Address, eg. 192.168.0.1")]
    $ServerIpAddress = "192.168.0.1",
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Internal Ip Range, eg. 192.168.0.0-192.168.0.255")]
    $InternalIpRange = "192.168.0.0-192.168.0.255"
)

#Import Exchange Certificate, and Enable it for POP IIS IMAP SMTP services.

Import-ExchangeCertificate  -FileData ([Byte[]]$(Get-content -Path $CertPath  -Encoding byte  -ReadCount 0)) -Password:$CertPassword -Force | Enable-ExchangeCertificate -Services 'POP, IIS, IMAP, SMTP' -Force

#New AcceptedDomain and set it to default

New-AcceptedDomain  -Name "official name"  -DomainName $domainname

Set-AcceptedDomain  -Identity "official name"  -MakeDefault $true

#New EmailAddress Policy

$address = "%m@" + $DomainName

New-EmailAddressPolicy -Name "Windows Server Essentials Email Address Policy" -IncludedRecipients AllRecipients -EnabledPrimarySMTPAddressTemplate $address

#Set owa and ecp VirtualDirectory ExternalUrl

$hostname = "mail." + $DomainName

$owa = "https://" + $hostname + "/owa"

$ecp = "https://" + $hostname + "/ecp"

$activesync = "https://" + $hostname + "/Microsoft-Server-ActiveSync"

$oab = "https://" + $hostname + "/OAB"

$ews = "https://" + $hostname + "/EWS/Exchange.asmx"

Get-OwaVirtualDirectory | Set-OwaVirtualDirectory  -ExternalUrl $owa  -InternalUrl $owa

Get-EcpVirtualDirectory | Set-EcpVirtualDirectory  -ExternalUrl $ecp  -InternalUrl $ecp

Get-ActiveSyncVirtualDirectory | Set-ActiveSyncVirtualDirectory -ExternalUrl $activesync  -InternalUrl $activesync

Get-OABVirtualDirectory | Set-OABVirtualDirectory -ExternalUrl $oab -InternalUrl $oab -RequireSSL:$true

Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -ExternalUrl $ews -InternalUrl $ews -BasicAuthentication:$True -Force

#Enable outlook Anywhere

Enable-OutlookAnywhere  -ClientAuthenticationMethod:Basic  -ExternalHostname:$hostname  -SSLOffloading:$false

#new receive/send connector

$machinename = get-content env:computername

$bindingIpaddress = $ServerIpAddress + ":25"

$ReceiveConnectorName = $machinename + "\Default " + $machinename

Set-ReceiveConnector $ReceiveConnectorName -RemoteIPRanges $InternalIpRange

New-ReceiveConnector -Name "WSE Internet Receive Connector" -Usage "Internet" -Bindings $bindingIpaddress -Fqdn $hostname -Enabled $true -Server $machinename -AuthMechanism Tls,BasicAuth,BasicAuthRequireTLS,Integrated

New-SendConnector -Name "WSE Internet SendConnector" -Usage "Internet" -AddressSpaces 'SMTP:*;1' -IsScopedConnector $false -DNSRoutingEnabled $true -UseExternalDNSServersEnabled $true -SourceTransportServers $machinename
```

5. Задайте параметры в начале сценария в соответствии со своей сетевой средой.

6. Сохраните файл как **ConfigureExchange.ps1**.

7. Запустите Windows PowerShell от имени администратора.

8. В командной строке Windows PowerShell введите команду **Set-ExecutionPolicy RemoteSigned** и нажмите ВВОД.

9. Запустите сценарий **InstallDependencies.ps1**.

10. Перезапустите сервер и затем запустите Windows PowerShell от имени администратора.

11. В командной строке Windows PowerShell выполните следующий сценарий:

    `E:\setup.com /mode:install /roles:mb,ht,ca /OrganizationName:"First Organization"`

   > [!NOTE]
   >  Введите правильный путь к программе установки Exchange Server.

12. По завершении установки Exchange Server откройте командную консоль Exchange от имени администратора.

13. В командной строке Exchange Management Shell введите команду **Set-ExecutionPolicy RemoteSigned** и нажмите ВВОД.

14. Запустите сценарий **ConfigureExchange.ps1**.

15. Перезапустите сервер.

> [!NOTE]
>  Если вы решили использовать общедоступный SSL-сертификат вместо самостоятельно выданного сертификата, следуйте инструкциям, приведенным в разделе руководств по установке, чтобы создать запрос на сертификат и отправить его в выбранный центр сертификации. Вы можете также воспользоваться командлетом Exchange PowerShell для создания запроса сертификата. См. пример ниже.
>
>  `New-ExchangeCertificate -GenerateRequest -SubjectName "C=US, S=Washington, L=Redmond, O=contoso, OU=contoso, CN=mail.contoso.com" -DomainName mail.contoso.com -PrivateKeyExportable $true | Set-Content -path "c:\Docs\MyCertRequest.req"`
>
>  Настройте параметры сценария в соответствии с вашей сетевой средой.

## <a name="post-installation-tasks"></a>Задачи, выполняемые после установки
 В этом разделе описаны действия по настройке сервера, которые, возможно, придется выполнить после установки. Здесь приведены сведения, касающиеся настройки локального сервера Exchange Server в сети Windows Server Essentials network.

### <a name="add-the-public-email-domain-and-configure-the-email-address-policies"></a>Добавление общедоступного почтового домена и настройка политик адресов электронной почты

> [!NOTE]
>  Это обязательная задача в случае чистой установки. Если вы проводите миграцию с Windows Small Business Server, пропустите этот шаг.

 Необходимо указать почтовый домен в качестве обслуживаемого домена по умолчанию и затем настроить политику адресов электронной почты.

##### <a name="to-add-your-email-domain-as-the-default-accepted-domain"></a>Добавление почтового домена в качестве обслуживаемого домена по умолчанию

1.  Для добавления обслуживаемого домена выполните инструкции из статьи о сервере Exchange Server, посвященной [созданию обслуживаемого домена](https://go.microsoft.com/fwlink/p/?LinkId=249174) .

2.  Войдите в систему второго сервера с правами администратора, откройте консоль управления Exchange и перейдите на вкладку **Транспортный сервер-концентратор** в окне **Конфигурация организации**.

3.  В рабочей области консоли управления Exchange правой кнопкой мыши щелкните новый обслуживаемый домен и выберите **По умолчанию**.

4.  Для создания новой политики адресов электронной почты выполните инструкции из статьи о сервере Exchange Server, посвященной [созданию политики адресов электронной почты](https://go.microsoft.com/fwlink/p/?LinkId=249179) . Можно оставить без изменения все значения по умолчанию, кроме адреса электронной почты. В качестве адреса электронной почты укажите свой общедоступный почтовый домен.

### <a name="create-smtp-send-and-receive-connectors"></a>Создание соединителей отправки и получения SMTP

> [!NOTE]
>  Выполнение данной задачи является обязательным.

 Необходимо настроить соединители отправки и получения SMTP для передачи исходящих и входящих электронных сообщений.

 Чтобы создать соединитель отправки SMTP, выполните инструкции из статьи о сервере Exchange Server [Создание соединителя отправки SMTP](/previous-versions/office/exchange-server-2010/aa997285(v=exchg.141)).

 Чтобы создать соединитель получения SMTP, выполните инструкции из статьи о сервере Exchange Server [Создание соединителя получения SMTP](/previous-versions/office/exchange-server-2010/bb125159(v=exchg.141)).

 Также можно воспользоваться инструкциями по созданию соединителей отправки и получения при помощи командлетов Exchange PowerShell, приведенными ранее в этом документе.

### <a name="configure-the-network-router"></a>Настройка сетевого маршрутизатора

> [!NOTE]
>  Это обязательная задача в случае чистой установки. Если вы проводите миграцию с Windows Small Business Server, см. инструкции по настройке сети в статье [Миграция данных сервера на Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md).

 Как минимум, необходимо настроить следующие параметры портов на маршрутизаторе:

|Порт маршрутизатора|Конечный IP-адрес|Конечный порт|Примечание|
|-----------------|--------------------|----------------------|----------|
|25 (SMTP)|Внутренний IP-адрес локального сервера Exchange Server|25||
|80 (HTTP)|Внутренний IP-адрес сервера под управлением Windows Server Essentials|80||
|443 (HTTPS)|Внутренний IP-адрес сервера под управлением Windows Server Essentials|443||

 Если в вашей сети поддерживаются протоколы обмена сообщениями POP3 или IMAP, нужно также настроить перенаправление портов для этих протоколов. Связанную с этой задачей информацию см. в разделе **Серверы клиентского доступа** в статье [Справочник по сетевым портам Exchange](https://go.microsoft.com/fwlink/p/?LinkId=250773) в технической библиотеке Exchange Server.

> [!NOTE]
> - Рекомендуется настроить статические IP-адреса для сервера Windows Server Essentials и для второго сервера, работающего под управлением Exchange Server. Инструкции по настройке статического IP-адреса на компьютере с ОС Windows Server 2003 или Windows Server 2008 R2 см. в статье [Настройка статического IP-адреса](https://technet.microsoft.com/library/cc754203\(v=ws.10\).aspx) в технической библиотеке Windows Server.
>
>   **Примечание.** Параметр DNS-сервера всегда должен указывать на IP-адрес сервера, на котором работает Windows Server Essentials.
>   -   IP-адреса сервера Windows Server Essentials и сервера Exchange Server на маршрутизаторе должны быть либо зарезервированы, либо находиться вне диапазона IP-адресов DHCP.
>   -   Конфигурация маршрутизатора, приведенная в этом разделе, предполагает, что поставщик услуг Интернета назначил для вас только один общий IP-адрес. Если у вас несколько общих IP-адресов, вы можете назначить другие IP-адреса серверу Windows Server Essentials и серверу Exchange Server, а затем создать перенаправление портов на основе общих IP-адресов.

### <a name="enable-on-premises-exchange-server-integration-on-windows-server-essentials"></a>Включить интеграцию локального Exchange Server в Windows Server Essentials

> [!NOTE]
>  Если вы проводите миграцию с Windows Small Business Server, рекомендуется пока пропустить этот шаг и выполнить его после удаления предыдущей установки Exchange Server на исходном сервере.

 После установки и настройки сервера Exchange Server необходимо включить интеграцию локального сервера Exchange Server на сервере Windows Server Essentials.

##### <a name="to-enable-on-premises-exchange-server-integration-from-the-dashboard"></a>Включение интеграции локального сервера Exchange Server с панели мониторинга

1.  Войдите в систему сервера под управлением Windows Server Essentials с правами администратора и откройте панель мониторинга.

2.  На **домашней странице** щелкните **Подключиться к службе электронной почты** и выберите **Интеграция сервера Exchange Server**.

3.  В области сведений щелкните **Настройка интеграции сервера Exchange Server**.

4.  Следуйте инструкциям мастера.

### <a name="configure-a-reverse-proxy"></a>Настройка обратного прокси-сервера

> [!NOTE]
>  Это действие обязательно для выполнения, если поставщик услуг Интернета предоставляет вам только одно подключение к Интернету.

 Как Windows Server Essentials, так и Exchange Server поддерживают несколько сценариев удаленного доступа для пользователей сети. Например, включив повсеместный доступ на сервере Windows Server Essentials, можно удаленно обращаться к сайту удаленного веб-доступа или использовать виртуальную частную сеть (VPN) для удаленного подключения к сети Windows Server Essentials. Для удаленного доступа к сообщениям электронной почты необходимо использовать мобильный Outlook, Outlook Web Access (OWA) или ActiveSync.

 Если и Windows Server Essentials, и сервер Exchange Server подключены к одному и тому же маршрутизатору и поставщик услуг Интернета предоставляет только одно входящее интернет-подключение для маршрутизатора, необходимо использовать обратный прокси-сервер для перенаправления различных типов поступающих из Интернета запросов удаленного доступа на основе имен узлов назначения. В качестве обратного прокси-сервера рекомендуется использовать поддерживаемое Майкрософт расширение "Маршрутизация запросов приложений" служб IIS. Дополнительную информацию о маршрутизации запросов приложений служб IIS см. на [веб-сайте маршрутизации запросов приложений](https://go.microsoft.com/fwlink/p/?LinkId=249181).

##### <a name="to-install-and-configure-application-request-routing"></a>Установка и настройка модуля маршрутизации запросов приложений

1. Войдите в Windows Server Essentials в качестве администратора.

2. Откройте браузер и перейдите на [веб-сайт маршрутизации запросов приложений](https://go.microsoft.com/fwlink/p/?LinkId=249181).

3. Для установки маршрутизации запросов приложений нажмите **Установить** и следуйте инструкциям.

   > [!NOTE]
   >  Во время установки необходимо выбрать модуль переопределения URL-адресов.
   >
   >  По завершении установки может появиться сообщение о том, что не удалось установить исправление из статьи базы знаний (KB 2589179) для модуля маршрутизации запросов приложений версии 2.5. Эту ошибку можно игнорировать.

4. По завершении установки модуля маршрутизации запросов приложений перезапустите службу **Шлюз удаленных рабочих столов**, если она не работает.

   > [!NOTE]
   >  После установки модуля маршрутизации запросов приложений служба **Шлюз удаленных рабочих столов** может быть остановлена. Чтобы вручную перезапустить службу, откройте средство администрирования **Службы** и перезапустите службу **Шлюз удаленных рабочих столов**.

5. [Загрузите KB 2732764 для модуля маршрутизации запросов приложений версии 2.5](https://go.microsoft.com/fwlink/?LinkID=258302)и установите обновление на сервер под управлением Windows Server Essentials.

6. Скопируйте файл сертификата SSL для Exchange Server на сервер Windows Server Essentials. Файл сертификата должен содержать закрытый ключ и иметь формат PFX.

   > [!NOTE]
   >  Если вы используете самостоятельно выданный сертификат, экспортируйте его, следуя инструкциям из статьи о сервере Exchange Server [Экспорт сертификата Exchange](/previous-versions/office/exchange-server-2010/dd351274(v=exchg.141)) .

7. В зависимости от используемой версии Windows Server Essentials выполните одно из следующих действий.

   -   В Windows Server Essentials: Откройте командное окно от имени администратора, а затем откройте каталог%Програмфилес%\виндовс Server\bin.

   -   В Windows Server Essentials: Откройте командное окно от имени администратора, а затем откройте каталог%Windir%\System32\Essentials.

8. В зависимости от варианта установки выполните один из следующих шагов для настройки маршрутизации запросов приложений:

   - В случае чистой установки выполните следующую команду:

      `ARRConfig config  -cert`_путь к файлу сертификата_ `-hostnames` _имена узлов для Exchange Server_

     > [!NOTE]
     >  Например: `ARRConfig config  -cert` _c:\temp\certificate.pfx_ `-hostnames` _mail.contoso.com_
     >
     >  Замените *mail.contoso.com* именем вашего домена, для которого выдан сертификат.

   - В случае миграции с Windows Small Business Server выполните следующую команду:

      `ARRConfig config  -cert`_путь к файлу сертификата_ `-hostnames` _имена узлов для Exchange Server_ `-targetserver` _имя сервера Exchange Server_

      Например, `ARRConfig config  -cert` _к:\темп\цертификате.пфкс_ `-hostnames` _mail.contoso.com_ `-targetserver` _ексчанжесвр_

      Замените *mail.contoso.com* именем вашего домена. Замените *ExchangeSvr* именем вашего сервера Exchange Server.

9. При появлении запроса введите пароль для сертификата.

> [!NOTE]
> - Имена узлов, которые вы указываете, должны содержаться в сертификате SSL, приобретенном для Exchange Server.
>   -   Если у вас несколько имен узлов, разделяйте их запятыми.

 Чтобы убедиться, что конфигурация работает, попытайтесь получить доступ к веб-сайту OWA для сервера, на котором работает Exchange Server ( https://mail . *имя вашего домена*.com/owa) с компьютера, не входящего в домен. Чтобы устранить неполадки подключения, можно также использовать средство [Анализатор удаленных подключений Майкрософт](https://go.microsoft.com/fwlink/p/?LinkId=249455) в Интернете.

### <a name="configure-split-dns-for-exchange-server"></a>Настройка разделения DNS для Exchange Server

> [!NOTE]
>  Это рекомендуемая задача.

 Разделение DNS позволяет настроить разные IP-адреса в DNS для одного и того же имени узла в зависимости от источника DNS-запроса. Если клиентский компьютер находится в интрасети, DNS-запрос разрешается в IP-адрес в интрасети. Если клиентский компьютер находится в Интернете, DNS-запрос разрешается в IP-адрес в Интернете. Этот процесс прозрачен для пользователей.

 Рекомендуется настроить разделение DNS таким образом, чтобы пользователи всегда могли использовать одно и то же имя узла для доступа к службам Exchange Server независимо от своего местоположения.

##### <a name="to-configure-split-dns-for-exchange-server"></a>Настройка разделения DNS для Exchange Server

1.  Войдите в Windows Server Essentials с правами администратора и откройте диспетчер DNS.

2.  В дереве консоли диспетчера DNS щелкните правой кнопкой мыши свой сервер и выберите **Новая зона**. Откроется **мастер создания новой зоны**.

3.  На странице **Тип зоны**, не изменяя заданное по умолчанию значение, нажмите кнопку **Далее**.

4.  На странице **Область репликации зоны, интегрированной в Active Directory**, не изменяя заданное по умолчанию значение, нажмите кнопку **Далее**.

5.  На странице **Зона прямого или обратного просмотра** примите или выберите вариант **Зона прямого просмотра** и нажмите кнопку **Далее**.

6.  На странице **Имя зоны** введите полное доменное имя вашего сервера Exchange Server (например, *mail.contoso.com*) и нажмите кнопку **Далее**.

7.  На странице **Динамическое обновление**, не изменяя заданное по умолчанию значение, нажмите кнопку **Далее**, а затем кнопку **Готово**.

8.  В дереве консоли диспетчера DNS щелкните правой кнопкой мыши новую зону прямого просмотра и выберите **Новый узел (А или АААА)**.

9. На странице **Новый узел** оставьте поле **Имя** пустым, введите IP-адрес вашего сервера Exchange Server в интрасети и нажмите кнопку **Добавить узел**.

    > [!NOTE]
    >  Если оставить поле **Имя** пустым, сервер будет использовать имя родительского домена по умолчанию.

10. На странице **Новый узел** нажмите кнопку **Готово**.

> [!NOTE]
>  Если вы используете ActiveSync, но не можете синхронизировать электронную почту для некоторых учетных записей, определите, являются ли эти учетные записи членами одной или нескольких защищенных групп, таких как "Администраторы домена". Дополнительные сведения, которые могут помочь в решении этой проблемы, см. в статье [Служба Exchange ActiveSync возвратила ошибку HTTP 500](https://technet.microsoft.com/library/dd439375\(EXCHG.80\).aspx).

## <a name="related-topics"></a>Связанные темы
 Дополнительные сведения об интеграции локального сервера Exchange:

### <a name="what-happens-if-i-disable-exchange-integration"></a>Что произойдет, если отключить интеграцию Exchange?
 Отключение интеграции с локальным сервером Exchange приведет к невозможности использовать панель мониторинга Windows Server Essentials для просмотра, создания и управления почтовыми ящиками Exchange Server.

### <a name="what-do-i-need-to-know-about-email-accounts"></a>Что нужно знать об учетных записях электронной почты?
 Хостинг электронной почты настраивается на вашем сервере. Решение из размещенного поставщика электронной почты, например Microsoft 365, может предоставлять индивидуальные учетные записи электронной почты для пользователей сети. При запуске мастер добавления учетных записей пользователей в Windows Server Essentials пытается добавить учетную запись пользователя с помощью доступной службы хостинга электронной почты. Одновременно мастер назначает пользователю имя (псевдоним) электронной почты и задает максимальный размер почтового ящика (квоту). Максимальный размер почтового ящика зависит от выбранного поставщика электронной почты. После добавления учетной записи пользователя, вы можете в дальнейшем управлять псевдонимом и информацией о квоте почтового ящика на странице настроек пользователя. Полное управление учетными записями пользователей и службой хостинга электронной почты осуществляется с помощью консоли управления. В зависимости от провайдера доступ к консоли управления осуществляется или через веб-портал, или через закладку в панели мониторинга.

 Псевдоним, указанный вами при запуске мастера добавления учетных записей пользователей, отправляется провайдеру как предлагаемое имя для псевдонима пользователя. Например, если псевдоним пользователя — *франкм*, то адрес электронной почты пользователя может быть <em>FrankM@Contoso.com</em> .

 Кроме того, пароль, который вы установите для пользователя в мастере добавления учетных записей пользователей, будет использоваться в качестве исходного пароля пользователя в хостинге электронной почты.

 Наконец, при удалении пользователя на сервере с помощью мастера удаления учетных записей пользователя мастер одновременно отправит запрос провайдеру хостинга электронной почты на удаление пользователя из системы. Поставщик может удалить учетную запись пользователя и электронное письмо, связанное с этой учетной записью.

 Дополнительные сведения об установке необходимых клиентских приложений электронной почты, а также о доступе к учетной записи электронной почты, содержатся в справочной документации, предоставляемой провайдером хостинга электронной почты.

### <a name="what-is-a-mailbox-quota"></a>Что такое квота электронной почты?
 Объем дискового пространства, выделяемый для данных почтового ящика Exchange пользователя сети, называется квотой почтовых ящиков.

 При выборе раздела **Настройки интеграции сервера Exchange Server** на панели мониторинга мастер добавляет страницу мастера добавления учетных записей пользователей, что позволяет в дальнейшем вводить квоты почтовых ящиков и устанавливать размер квот. По умолчанию параметр **Применять квоты почтовых ящиков** установлен (включен), и для почтовых ящиков пользователей предоставляется 2 ГБ дискового пространства. Администраторы Exchange могут настраивать размер квоты почтовых ящиков с учетом бизнес-потребностей.

## <a name="additional-references"></a>Дополнительные ссылки

-   [Системные требования к Windows Server Essentials](../get-started/system-requirements.md)

-   [Управление интеграцией со службой электронной почты](Manage-Email-Service-Integration-in-Windows-Server-Essentials.md)

-   [Управление Windows Server Essentials](Manage-Windows-Server-Essentials.md)