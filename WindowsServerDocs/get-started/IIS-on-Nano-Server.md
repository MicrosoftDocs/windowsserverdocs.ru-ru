---
title: IIS на сервере Nano Server
description: Сведения о настройке IIS на сервере Nano Server
manager: DonGill
ms.topic: article
ms.date: 09/06/2017
ms.assetid: 16984724-2d77-4d7b-9738-3dff375ed68c
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: b5b469e3aa2e3cb3eb9f050667450be48da03b15
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87959722"
---
# <a name="iis-on-nano-server"></a>IIS на сервере Nano Server

> Область применения. Windows Server 2016

> [!IMPORTANT]
> Начиная с Windows Server версии 1709, сервер Nano Server будет доступен только в качестве [базового образа ОС контейнера](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image). Его описание см. в статье об [изменениях сервера Nano Server](nano-in-semi-annual-channel.md).

Вы можете установить роль сервера служб IIS на сервере Nano Server, используя параметр -Package с Microsoft-NanoServer-IIS-Package. Дополнительные сведения о настройке сервера Nano Server, включая установку пакетов, см. в статье [Установка сервера Nano Server](Getting-Started-with-Nano-Server.md).

В этом выпуске Nano Server доступны следующие функции служб IIS:

|Функция|По умолчанию включено|
|-----------|----------------------|
|**Общие компоненты HTTP**||
|Документ по умолчанию|x|
|Просмотр каталогов|x|
|Ошибки HTTP|x|
|Статическое содержимое|x|
|Перенаправление HTTP||
|**Работоспособность и диагностика**||
|Ведение журнала HTTP|x|
|Настраиваемое протоколирование||
|Монитор запросов||
|Трассировка||
|**Производительность**||
|Сжатие статического содержимого|x|
|Сжатие динамического содержимого||
|**Безопасность**||
|Фильтрация запросов|x|
|Обычная проверка подлинности||
|Проверка подлинности с сопоставлением сертификата клиента||
|Дайджест-проверка подлинности||
|Проверка подлинности с сопоставлением сертификата клиента IIS||
|Ограничения IP-адресов и имен домена||
|Авторизация URL-адреса||
|Проверка подлинности Windows||
|**Разработка приложений**||
|Инициализация приложений||
|CGI||
|Расширения ISAPI||
|Фильтры ISAPI||
|Серверные включаемые модули||
|Протокол WebSocket||
|**Инструменты управления**||
|Модуль IISAdministration для Windows PowerShell|x|

Цикл статей о других конфигурациях служб IIS (например, с использованием ASP.NET, PHP и Java), а также другие материалы по этой теме опубликованы здесь: [https://iis.net/learn](https://iis.net/learn).

## <a name="installing-iis-on-nano-server"></a>Установка служб IIS на сервере Nano Server
Эту роль сервера можно установить либо в автономном режиме (при отключенном Nano Server), либо в сети (с использованием Nano Server). Рекомендуется установка в автономном режиме.

Для автономной установки добавьте пакет с параметром -Packages New-NanoServerImage, как в следующем примере:

```PowerShell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1.vhd -ComputerName Nano1 -Package Microsoft-NanoServer-IIS-Package
```

Если имеется существующий файл виртуального жесткого диска, можно установить службы IIS в автономном режиме с помощью DISM.exe, подключив виртуальный жесткий диск, а затем воспользовавшись параметром **Add-Package**.
В следующем примере предполагается, что запуск осуществляется из каталога, заданного параметром BasePath и созданного после выполнения New-NanoServerImage.

1. mkdir mountdir
2. .\Tools\dism.exe /Mount-Image /ImageFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir
3. .\Tools\dism.exe /Add-Package /PackagePath:.\packages\Microsoft-NanoServer-IIS-Package.cab /Image:.\mountdir
4. .\Tools\dism.exe /Add-Package /PackagePath:.\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab /Image:.\mountdir
5. .\Tools\dism.exe /Unmount-Image /MountDir:.\MountDir /Commit


> [!NOTE]
> Обратите внимание, что шаг 4 добавляет языковой пакет, в этом примере — для языка EN-US.

На этом этапе можно запустить Nano Server со службами IIS.

### <a name="installing-iis-on-nano-server-online"></a>Установка служб IIS на сервере Nano Server в сети
Хотя для этой роли сервера рекомендуется автономная установка, в сценариях с контейнерами может потребоваться установить ее в сети (с Nano Server). Для этого выполните следующие действия:

1. Скопируйте папку Packages с установочного носителя на запущенный сервер Nano Server (например, в C:\packages).

2. Создайте файл Unattend.xml на другом компьютере и скопируйте его на сервер Nano Server. Можете скопировать и вставить в созданный файл это XML-содержимое:


```
    <unattend xmlns=urn:schemas-microsoft-com:unattend>
    <servicing>
        <package action=install>
            <assemblyIdentity name=Microsoft-NanoServer-IIS-Package version=10.0.14393.0 processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral />
            <source location=c:\packages\Microsoft-NanoServer-IIS-Package.cab />
        </package>
        <package action=install>
            <assemblyIdentity name=Microsoft-NanoServer-IIS-Package version=10.0.14393.0 processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=en-US />
            <source location=c:\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab />
        </package>
    </servicing>
    <cpi:offlineImage cpi:source= xmlns:cpi=urn:schemas-microsoft-com:cpi />
</unattend>
```


3. В новом XML-файле, который вы создали (или скопировали), измените C:\packages на каталог, куда вы скопировали содержимое папки Packages.

4. Перейдите в каталог с недавно созданным XML-файлом и выполните команду

   **dism /online /apply-unattend:.\unattend.xml**


5. Убедитесь, что пакет IIS и связанный с ним языковой пакет установлены правильно, выполнив следующую команду:

   **dism /online /get-packages**

   Вы должны увидеть идентификатор пакета: Microsoft-NanoServer-IIS-Package~31bf3856ad364e35~amd64~~10.0.14393.1000, указанный дважды (для элементов "Тип выпуска: Языковый пакет" и "Тип выпуска: Пакет функций".

6. Запустите службу W3SVC либо с помощью команды **net start w3svc**, либо перезапустив Nano Server.

## <a name="starting-iis"></a>Запуск служб IIS
После установки и запуска служб IIS все готово к обработке веб-запросов. Убедитесь, что службы IIS запущены, перейдя на веб-страницу служб IIS по умолчанию по адресу http://\<IP address of Nano Server>. На физическом компьютере IP-адрес можно определить с помощью агента восстановления. На виртуальной машине IP-адрес можно получить, используя командную строку Windows PowerShell и выполнив следующую команду:

```PowerShell
Get-VM -name <VM name> | Select -ExpandProperty networkadapters | select IPAddresses
```

Если не удается получить доступ к веб-странице IIS по умолчанию, перепроверьте установку служб IIS, просмотрев каталог **c:\inetpub** на сервере Nano Server.

## <a name="enabling-and-disabling-iis-features"></a>Включение и отключение функций IIS
Ряд функций IIS включается по умолчанию при установке роли IIS (см. таблицу в разделе "Обзор служб IIS на сервере Nano Server" этой статьи). Включить (или отключить) дополнительные функции можно с помощью DISM.exe.

Каждая из функций служб IIS существует в виде набора элементов конфигурации. Например, функция проверки подлинности Windows включает в себя следующие элементы:

|Раздел|Элементы конфигурации|
|-----------|--------------------------|
|`<globalModules>`|`<add name=WindowsAuthenticationModule image=%windir%\System32\inetsrv\authsspi.dll`|
|`<modules>`|`<add name=WindowsAuthenticationModule lockItem=true \/>`|
|`<windowsAuthentication>`|`<windowsAuthentication enabled=false authPersistNonNTLM\=true><providers><add value=Negotiate /><add value=NTLM /><br /></providers><br /></windowsAuthentication>`|

Полный набор вложенных функций IIS приведен в приложении 1 этой статьи, а соответствующие элементы конфигурации указаны в приложении 2.


### <a name="example-installing-windows-authentication"></a>Пример: установка проверки подлинности Windows

1. Откройте консоль удаленного сеанса Windows PowerShell на сервере Nano Server.

2. Используйте `DISM.exe` для установки модуля проверки подлинности Windows:

    ```
    dism /Enable-Feature /online /featurename:IIS-WindowsAuthentication /all
    ```

    Параметр `/all` установит любой компонент, от которого зависит выбранная функция.

### <a name="example-uninstalling-windows-authentication"></a>Пример: удаление проверки подлинности Windows

1. Откройте консоль удаленного сеанса Windows PowerShell на сервере Nano Server.

2. Используйте `DISM.exe` для удаления модуля проверки подлинности Windows:

    ```
    dism /Disable-Feature /online /featurename:IIS-WindowsAuthentication
    ```

## <a name="other-common-iis-configuration-tasks"></a>Другие стандартные задачи настройки IIS
**Создание веб-сайтов**

Используйте следующий командлет:

`PS D:\> New-IISSite -Name TestSite -BindingInformation *:80:TestSite -PhysicalPath c:\test`

Затем можно запустить `Get-IISSite` для проверки состояния сайта (возвращает имя веб-сайта, идентификатор, состояние, физический путь и привязки).

**Удаление веб-сайтов**

Выполните команду `Remove-IISSite -Name TestSite -Confirm:$false`.

**Создание виртуальных каталогов**

Можно создать виртуальные каталоги с помощью объекта IISServerManager, возвращенного Get-IISServerManager, который предоставляет API .NET Microsoft.Web.Administration.ServerManager. В этом примере указанные команды обращаются к элементу "Веб-сайт по умолчанию" коллекции сайтов и корневому элементу приложения (/) раздела приложений. Затем они вызывают метод Add() коллекции VirtualDirectories для этого элемента приложения, чтобы создать новый каталог:

```PowerShell
PS C:\> $sm = Get-IISServerManager
PS C:\> $sm.Sites["Default Web Site"].Applications[/].VirtualDirectories.Add(/DemoVirtualDir1, c:\test\virtualDirectory1)
PS C:\> $sm.Sites["Default Web Site"].Applications[/].VirtualDirectories.Add(/DemoVirtualDir2, c:\test\virtualDirectory2)
PS C:\> $sm.CommitChanges()
```

**Создание пулов приложений**

Аналогичным образом можно использовать Get-IISServerManager для создания пулов приложений:

```PowerShell
PS C:\> $sm = Get-IISServerManager
PS C:\> $sm.ApplicationPools.Add(DemoAppPool)
```

**Настройка HTTPS и сертификатов**

Используйте программу Certoc.exe для импорта сертификатов, как в этом примере, где показана настройка HTTPS для веб-сайта на сервере Nano Server:

1. На другом компьютере, где не выполняется Nano Server, создайте сертификат (с использованием собственного имени сертификата и пароля) и экспортируйте его в c:\temp\test.pfx.

    `$newCert = New-SelfSignedCertificate -DnsName www.foo.bar.com -CertStoreLocation cert:\LocalMachine\my`

    `$mypwd = ConvertTo-SecureString -String YOUR_PFX_PASSWD -Force -AsPlainText`

    `Export-PfxCertificate -FilePath c:\temp\test.pfx -Cert $newCert -Password $mypwd`

2. Скопируйте файл test.pfx на компьютер Nano Server.

3. На сервере Nano Server импортируйте сертификат в хранилище MY с помощью следующей команды:

    **certoc.exe -ImportPFX -p YOUR_PFX_PASSWD My c:\temp\test.pfx**

4. Извлеките отпечаток нового сертификата (в данном примере это 61E71251294B2A7BB8259C2AC5CF7BA622777E73) с помощью `Get-ChildItem Cert:\LocalMachine\my`.

5. Добавьте привязку HTTPS на веб-сайт по умолчанию (или любой веб-сайт, на который требуется добавить привязку) с помощью следующих команд Windows PowerShell:

    ```PowerShell
    $certificate = get-item Cert:\LocalMachine\my\61E71251294B2A7BB8259C2AC5CF7BA622777E73
    # Use your actual thumbprint instead of this example
    $hash = $certificate.GetCertHash()

    Import-Module IISAdministration
    $sm = Get-IISServerManager
    $sm.Sites["Default Web Site"].Bindings.Add("*:443:", $hash, "My", "0")    # My is the certificate store name
    $sm.CommitChanges()
    ```

    Можно также использовать указание имени сервера (SNI) с именем конкретного узла, применив следующий синтаксис: `$sm.Sites["Default Web Site"].Bindings.Add("*:443:www.foo.bar.com", $hash, "My", "SNI")`

## <a name="appendix-1-list-of-iis-sub-features"></a>Приложение 1. Список вложенных функций IIS

- IIS-WebServer
- IIS-CommonHttpFeatures
- IIS-StaticContent
- IIS-DefaultDocument
- IIS-DirectoryBrowsing
- IIS-HttpErrors
- IIS-HttpRedirect
- IIS-ApplicationDevelopment
- IIS-CGI
- IIS-ISAPIExtensions
- IIS-ISAPIFilter
- IIS-ServerSideIncludes
- IIS-WebSockets
- IIS-ApplicationInit
- IIS-Security
- IIS-BasicAuthentication
- IIS-WindowsAuthentication
- IIS-DigestAuthentication
- IIS-ClientCertificateMappingAuthentication
- IIS-IISCertificateMappingAuthentication
- IIS-URLAuthorization
- IIS-RequestFiltering
- IIS-IPSecurity
- IIS-CertProvider
- IIS-Performance
- IIS-HttpCompressionStatic
- IIS-HttpCompressionDynamic
- IIS-HealthAndDiagnostics
- IIS-HttpLogging
- IIS-LoggingLibraries
- IIS-RequestMonitor
- IIS-HttpTracing
- IIS-CustomLogging

## <a name="appendix-2-elements-of-http-features"></a>Приложение 2. Элементы функций HTTP
Каждая из функций служб IIS существует в виде набора элементов конфигурации. Это приложение содержит список элементов конфигурации для всех функций в данном выпуске Nano Server.

### <a name="common-http-features"></a>Общие компоненты HTTP
**Документ по умолчанию**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=DefaultDocumentModule image=%windir%\System32\inetsrv\defdoc.dll />`|
|`<modules>`|`<add name=DefaultDocumentModule lockItem=true />`|
|`<handlers>`|`<add name=StaticFile path=* verb=* modules=DefaultDocumentModule resourceType=EiSecther requireAccess=Read />`|
|`<defaultDocument>`|`<defaultDocument enabled=true><br /><files><br /> <add value=Default.htm /><br />        <add value=Default.asp /><br />        <add value=index.htm /><br />        <add value=index.html /><br />        <add value=iisstart.htm /><br />    </files><br /></defaultDocument>`|

Запись `StaticFile <handlers>` может уже присутствовать. В этом случае просто добавьте DefaultDocumentModule в атрибут \<modules>, отделив значение запятой.

**Просмотр каталогов**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=DirectoryListingModule image=%windir%\System32\inetsrv\dirlist.dll />`|
|`<modules>`|`<add name=DirectoryListingModule lockItem=true />`|
|`<handlers>`|`<add name=StaticFile path=* verb=* modules=DirectoryListingModule resourceType=Either requireAccess=Read />`|

Запись `StaticFile <handlers>` может уже присутствовать. В этом случае просто добавьте DirectoryListingModule в атрибут \<modules>, отделив значение запятой.

**Ошибки HTTP**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=CustomErrorModule image=%windir%\System32\inetsrv\custerr.dll />`|
|`<modules>`|`<add name=CustomErrorModule lockItem=true />`|
|`<httpErrors>`|`<httpErrors lockAttributes=allowAbsolutePathsWhenDelegated,defaultPath><br />    <error statusCode=401    prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=401.htm ><br />    <error statusCode=403 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=403.htm /><br />    <error statusCode=404 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=404.htm /><br />    <error statusCode=405 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=405.htm /><br />    <error statusCode=406 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=406.htm /><br />    <error statusCode=412 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=412.htm /><br />    <error statusCode=500 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=500.htm /><br />    <error statusCode=501 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=501.htm /><br />    <error statusCode=502 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=502.htm /><br /></httpErrors>`|

**Статическое содержимое**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=StaticFileModule image=%windir%\System32\inetsrv\static.dll />`|
|`<modules>`|`<add name=StaticFileModule lockItem=true />`|
|`<handlers>`|`<add name=StaticFile path=* verb=* modules=StaticFileModule resourceType=Either requireAccess=Read />`|

Запись `StaticFile \<handlers>` может уже присутствовать. В этом случае просто добавьте StaticFileModule в атрибут \<modules>, отделив значение запятой.

**Перенаправление HTTP**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=HttpRedirectionModule image=%windir%\System32\inetsrv\redirect.dll />`|
|`<modules>`|`<add name=HttpRedirectionModule lockItem=true />`|
|`<httpRedirect>`|`<httpRedirect enabled=false />`|

### <a name="health-and-diagnostics"></a>Работоспособность и диагностика
**Ведение журнала HTTP**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=HttpLoggingModule image=%windir%\System32\inetsrv\loghttp.dll />`|
|`<modules>`|`<add name=HttpLoggingModule lockItem=true />`|
|`<httpLogging>`|`<httpLogging dontLog=false />`|

**Настраиваемое ведение журнала**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=CustomLoggingModule image=%windir%\System32\inetsrv\logcust.dll />`|
|`<modules>`|`<add name=CustomLoggingModule lockItem=true />`|

**Монитор запросов**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=RequestMonitorModule image=%windir%\System32\inetsrv\iisreqs.dll />`|

**Трассировка**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=TracingModule image=%windir%\System32\inetsrv\iisetw.dll \/><br /><add name=FailedRequestsTracingModule image=%windir%\System32\inetsrv\iisfreb.dll />`|
|`<modules>`|`<add name=FailedRequestsTracingModule lockItem=true />`|
|`<traceProviderDefinitions>`|`<traceProviderDefinitions><br />    <add name=WWW Server guid\={3a2a4e84-4c21-4981-ae10-3fda0d9b0f83}><br />        <areas><br />            <clear /><br />            <add name=Authentication value=2 /><br />            <add name=Security value=4 /><br />            <add name=Filter value=8 /><br />            <add name=StaticFile value=16 /><br />            <add name=CGI value=32 /><br />            <add name=Compression value=64 /><br />            <add name=Cache value=128 /><br />            <add name=RequestNotifications value=256 /><br />            <add name=Module value=512 /><br />            <add name=FastCGI value=4096 /><br />            <add name=WebSocket value=16384 /><br />        </areas><br />    </add><br />    <add name=ISAPI Extension guid={a1c2040e-8840-4c31-ba11-9871031a19ea}><br />        <areas><br />            <clear /><br />        </areas><br />    </add><br /></traceProviderDefinitions>`|

### <a name="performance"></a>Производительность
**Сжатие статического содержимого**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=StaticCompressionModule image=%windir%\System32\inetsrv\compstat.dll />`|
|`<modules>`|`<add name=StaticCompressionModule lockItem=true />`|
|`<httpCompression>`|`<httpCompression directory=%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files><br />    <scheme name=gzip dll=%Windir%\system32\inetsrv\gzip.dll /><br />   <staticTypes><br />        <add mimeType=text/* enabled=true /><br />        <add mimeType=message/* enabled=true /><br />        <add mimeType=application/javascript enabled=true \/><br />        <add mimeType=application/atom+xml enabled=true /><br />        <add mimeType=application/xaml+xml enabled=true /><br />        <add mimeType=\*\* enabled=false /><br />    </staticTypes><br /></httpCompression>`|

**Сжатие динамического содержимого**

|Раздел|Элементы конфигурации|
|-----------|--------------------------|
|`<globalModules>`|`<add name=DynamicCompressionModule image=%windir%\System32\inetsrv\compdyn.dll />`|
|`<modules>`|`<add name=DynamicCompressionModule lockItem=true />`|
|`<httpCompression>`|`<httpCompression directory\=%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files><br />    <scheme name=gzip dll=%Windir%\system32\inetsrv\gzip.dll \/><br />    \<dynamicTypes><br />        <add mimeType=text/* enabled=true \/><br />        <add mimeType=message/* enabled=true /><br />        <add mimeType=application/x-javascript enabled=true /><br />        <add mimeType=application/javascript enabled=true /><br />        <add mimeType=*/* enabled=false /><br />    <\/dynamicTypes><br /></httpCompression>`|

### <a name="security"></a>Безопасность
**Фильтрация запросов**


|       Раздел        |                                                                                                                                        Элементы конфигурации                                                                                                                                        |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  `<globalModules>`   |                                                                                                        `<add name=RequestFilteringModule image=%windir%\System32\inetsrv\modrqflt.dll />`                                                                                                        |
|     `<modules>`      |                                                                                                                       `<add name=RequestFilteringModule lockItem=true />`                                                                                                                        |
| \`<requestFiltering> | `<requestFiltering><br />    <fileExtensions allowUnlisted=true applyToWebDAV=true /><br />    <verbs allowUnlisted=true applyToWebDAV=true /><br />    <hiddenSegments applyToWebDAV=true><br />        <add segment=web.config /><br />    </hiddenSegments><br /></requestFiltering>` |

**Обычная проверка подлинности**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=BasicAuthenticationModule image=%windir%\System32\inetsrv\authbas.dll />`|
|`<modules>`|`<add name=WindowsAuthenticationModule lockItem=true />`|
|`<basicAuthentication>`|`<basicAuthentication enabled=false />`|

**Аутентификация с сопоставлением сертификата клиента**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=CertificateMappingAuthentication image=%windir%\System32\inetsrv\authcert.dll />`|
|`<modules>`|`<add name=CertificateMappingAuthenticationModule lockItem=true />`|
|`<clientCertificateMappingAuthentication>`|`<clientCertificateMappingAuthentication enabled=false />`|

**Дайджест-аутентификация**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=DigestAuthenticationModule image=%windir%\System32\inetsrv\authmd5.dll />`|
|`<modules>`|`<add name=DigestAuthenticationModule lockItem=true />`|
|`<other>`|`<digestAuthentication enabled=false />`|

**Аутентификация с сопоставлением сертификата клиента IIS**


|                  Раздел                   |                                         Элементы конфигурации                                         |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------|
|             `<globalModules>`              | `<add name=CertificateMappingAuthenticationModule image=%windir%\System32\inetsrv\authcert.dll />` |
|                `<modules>`                 |               `<add name=CertificateMappingAuthenticationModule lockItem=true `/>\`                |
| `<clientCertificateMappingAuthentication>` |                      `<clientCertificateMappingAuthentication enabled=false />`                      |

**Ограничения IP-адресов и доменов**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|```<add name=IpRestrictionModule image=%windir%\System32\inetsrv\iprestr.dll /><br /><add name=DynamicIpRestrictionModule image=%windir%\System32\inetsrv\diprestr.dll />```|
|`<modules>`|`<add name=IpRestrictionModule lockItem=true \/><br /><add name=DynamicIpRestrictionModule lockItem=true \/>`|
|`<ipSecurity>`|`<ipSecurity allowUnlisted=true />`|

**Авторизация URL-адреса**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=UrlAuthorizationModule image=%windir%\System32\inetsrv\urlauthz.dll />`|
|`<modules>`|`<add name=UrlAuthorizationModule lockItem=true />`|
|`<authorization>`|`<authorization><br />    <add accessType=Allow users=* /><br /></authorization>`|

**Проверка подлинности Windows**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=WindowsAuthenticationModule image=%windir%\System32\inetsrv\authsspi.dll />`|
|`<modules>`|`<add name=WindowsAuthenticationModule lockItem=true />`|
|`<windowsAuthentication>`|`<windowsAuthentication enabled=false authPersistNonNTLM\=true><br />    <providers><br />        <add value=Negotiate /><br />        <add value=NTLM /><br />    <\providers><br /><\windowsAuthentication><windowsAuthentication enabled=false authPersistNonNTLM\=true><br />    <providers><br />        <add value=Negotiate /><br />        <add value=NTLM /><br />    <\/providers><br /><\/windowsAuthentication>`|

### <a name="application-development"></a>Разработка приложений
**Инициализация приложения**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=ApplicationInitializationModule image=%windir%\System32\inetsrv\warmup.dll />`|
|`<modules>`|`<add name=ApplicationInitializationModule lockItem=true />`|

**CGI**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=CgiModule image=%windir%\System32\inetsrv\cgi.dll /><br /><add name=FastCgiModule image=%windir%\System32\inetsrv\iisfcgi.dll />`|
|`<modules>`|`<add name=CgiModule lockItem=true /><br /><add name=FastCgiModule lockItem=true />`|
|`<handlers>`|`<add name=CGI-exe path=*.exe verb=\* modules=CgiModule resourceType=File requireAccess=Execute allowPathInfo=true />`|

**Расширения ISAPI**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=IsapiModule image=%windir%\System32\inetsrv\isapi.dll />`|
|`<modules>`|`<add name=IsapiModule lockItem=true />`|
|`<handlers>`|`<add name=ISAPI-dll path=*.dll verb=* modules=IsapiModule resourceType=File requireAccess=Execute allowPathInfo=true />`|

**Фильтры ISAPI**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=IsapiFilterModule image=%windir%\System32\inetsrv\filter.dll />`|
|`<modules>`|`<add name=IsapiFilterModule lockItem=true />`|

**Серверные включаемые модули**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|<`add name=ServerSideIncludeModule image=%windir%\System32\inetsrv\iis_ssi.dll />`|
|`<modules>`|`<add name=ServerSideIncludeModule lockItem=true />`|
|`<handlers>`|`<add name=SSINC-stm path=*.stm verb=GET,HEAD,POST modules=ServerSideIncludeModule resourceType=File \/><br /><add name=SSINC-shtm path=*.shtm verb=GET,HEAD,POST modules=ServerSideIncludeModule resourceType=File /><br /><add name=SSINC-shtml path=*.shtml verb=GET,HEAD,POST modules=ServerSideIncludeModule resourceType=File />`|
|`<serverSideInclude>`|`<serverSideInclude ssiExecDisable=false />`|

**Протокол WebSocket**

|Раздел|Элементы конфигурации|
|----------------|--------------------------|
|`<globalModules>`|`<add name=WebSocketModule image=%windir%\System32\inetsrv\iiswsock.dll />`|
|`<modules>`|`<add name=WebSocketModule lockItem=true />`|
