---
title: Развертывание режима Windows Server Essentials в качестве размещенного сервера
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: a455c6b4-b29f-4f76-8c6b-1578b6537717
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 0f47c3870ad8254fb1c8cf63fc8f4fd055235d50
ms.sourcegitcommit: 34f9577ef32cbdc7ef96040caabc9d83517f9b79
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2020
ms.locfileid: "89554507"
---
# <a name="deploy-windows-server-essentials-experience-as-a-hosted-server"></a>Развертывание режима Windows Server Essentials в качестве размещенного сервера

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Этот документ содержит сведения, относящиеся к поставщикам услуг размещения, которые планирует развернуть Microsoft Windows Server 16 с помощью роли Windows Server Essentials (Windows Server Essentials в оставшейся части документа), установленной в своей лаборатории, и предложит предложить Windows Server Essentials в качестве услуги своим клиентам. Данный документ содержит следующие разделы:


-   [Обзор возможностей Windows Server Essentials](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)

-   [Преимущества размещения Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)

-   [Поддерживаемые варианты развертывания](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)

-   [Поддерживаемые топологии сети](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)

-   [Настройка образа Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)

-   [Автоматизация развертывания Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)

-   [Миграция данных с Windows Small Business Server на Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)

-   [Выполнение общих задач с помощью Windows PowerShell](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)

-   [Интеграция электронной почты с Windows Server Essentials](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)

-   [Контроль и управление с помощью стандартных средств](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)

-   [Сценарии тестирования](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)

-   [Сведения о поддержке](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)


##  <a name="windows-server-essentials-experience-overview"></a><a name="BKMK_WSEEOverview"></a> Обзор возможностей Windows Server Essentials
 Интерфейс Windows Server Essentials — это роль сервера, доступная в центре обработки данных Windows Server 2012 R2 Standard и Windows Server 2012 R2. Если роль Windows Server Essentials Experience установлена на сервере под Windows Server 2012 R2, клиент может воспользоваться всеми функциями, доступными в Windows Server Essentials без блокировок и ограничений. Опыт работы с Windows Server Essentials позволяет выполнять следующие распределенные решения для малых и средних предприятий.

-   **Хранение и защита данных** Вы можете хранить данные клиента с в централизованном расположении и защищать данные сервера и клиента, создав резервную копию сервера и клиентских компьютеров (менее 75) в сети.

-   **Управление пользователями**. Управление пользователями и группами пользователей осуществляется через упрощенную панель мониторинга сервера. Кроме того, интеграция с Microsoft Azure Active Directory (Azure AD) обеспечивает простой доступ к данным для веб-службы Майкрософт (например, Microsoft 365, Exchange Online и SharePoint Online) для пользователей с использованием учетных данных домена.

-   **Интеграция службы** Сервер можно интегрировать с Microsoft веб-службы (например, Microsoft 365, SharePoint Online и Microsoft Azure Backup). Можно также интегрировать сервер с вашими службами и службами сторонних поставщиков.

-   **Повсеместный доступ**. Клиент имеет доступ к серверу, компьютерам сети и данным с любого устройства и из любой точки, где есть доступ к Интернету. Удаленный веб-доступ позволяет получить доступ к приложениям и данным с помощью простого и оптимизированного под сенсорные дисплеи браузерного интерфейса. Приложение My Server позволяет им получать доступ к данным из Windows Phone или Microsoft Store приложения.

-   **Потоковая передача мультимедиа** Если пакет мультимедиа устанавливается на сервере с включенным интерфейсом Windows Server Essentials, конечный пользователь может хранить музыку, видео и фотографии в общих папках, а затем получать доступ к этим файлам мультимедиа с сетевых компьютеров или удаленных Веб-доступ.

-   **Наблюдение за работоспособностью системы**. Можно отслеживать работоспособность сети и получать настраиваемые отчеты.

##  <a name="benefits-of-hosting-windows-server-essentials-experience"></a><a name="BKMK_Benefits"></a> Преимущества размещения Windows Server Essentials
  Windows Server Essentials — это роль в Windows Server, которая позволяет повторно использовать существующую среду развертывания и управления в Windows Server для развертывания и настройки роли Windows Server Essentials Experience. Размещение роли Windows Server Essentials обеспечивает следующие преимущества:

-   **Упрощенное развертывание** Просто включив роль Windows Server Essentials Experience, некоторые из наиболее часто используемых ролей и компонентов включаются и настраиваются с помощью рекомендаций для малых и средних предприятий. Можно настроить функции Windows Server Essentials или скрыть некоторые локальные функции. Если вы используете Windows Azure Pack, можно скачать шаблон коллекции для Windows Server Essentials в Windows Server 2012 R2.

-   **Упрощенная панель мониторинга**. Панель мониторинга Windows Server Essentials упрощает выполнение общих задач, таких как управление серверными папками и их хранение, резервное копирование и восстановление, управление учетными записями пользователей или групп пользователей, удаленным доступом и электронной почтой. Это дает возможность клиентам малого и среднего бизнеса выполнять повседневные задачи без необходимости обращения в службу технической поддержки.

-   **Расширяемость**. Панель мониторинга Windows Server Essentials и программное обеспечение Windows Server Essentials Connector расширяемы. Вы можете добавить свою собственную фирменную интеграцию, чтобы все клиенты имели одну точку входа для серверов и служб.

-   **Мониторинг**. Новая версия пакета мониторинга системного центра позволяет управлять несколькими серверами под управлением Windows Server Essentials. Сведения о загрузке пакета управления см. в разделе [пакет управления System Center для Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809).

##  <a name="supported-deployment-options"></a><a name="BKMK_SupportedDeployment"></a> Поддерживаемые варианты развертывания
  Интерфейс Windows Server Essentials можно развернуть как контроллер домена в новой Active Directory среде. Кроме того, его можно развернуть в существующей Active Directory среде как член домена.

 Рекомендуется сначала развернуть Windows Server 2012 R2 Standard или Windows Server 2012 R2 Datacenter, а затем установить роль Windows Server Essentials Experience. С помощью этого метода развертывания вы получаете все функциональные возможности Windows Server Essentials Edition без блокировок и ограничений.


 Дополнительные сведения об установке Windows Server 2012 R2 с ролью Windows Server Essentials см. в [статье Установка и настройка Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).



##  <a name="supported-network-topologies"></a><a name="BKMK_SupportedToplogy"></a> Поддерживаемые сетевые топологии
 Чтобы использовать интерфейс Windows Server Essentials из перемещаемого клиента, необходимо включить VPN. Чтобы включить удаленный доступ к серверу для мобильных клиентов, необходимо открыть на сервере порт 443 и порт 80.

 Ниже представлены две стандартные топологии сети на стороне сервера, а также настройки VPN и удаленного веб-доступа.

- **Топология 1** (это предпочтительный метод топологии, который помещает все серверы и диапазон IP-адресов VPN в одной подсети).

  -   Настройка сервера в отдельной виртуальной сети с помощью устройства преобразования сетевых адресов (NAT).

  -   Включение службы DHCP в виртуальной сети, либо назначение статического IP-адреса для сервера.

  -   Переадресация общего IP-порта 443 маршрутизатора на сетевой адрес сервера.

  -   Разрешение сквозного режима VPN для порта 443.

  -   Установка пула IPv4-адресов VPN в том же диапазоне подсети, что и адрес сервера.

  -   Назначение вторичным серверам статического IP-адреса в том же диапазоне подсети, но вне пула VPN-адресов.

- **Топология 2**:

  -   Назначение серверу частного IP-адреса.

  -   Разрешение доступа порту 443 на сервере к открытому порту 443 IP-адреса.

  -   Разрешение сквозного режима VPN для порта 443.

  -   Назначение различных диапазонов IPv4-адресов для VPN и для адреса сервера.

  В топологии 2 не поддерживаются функции вторичного сервера, поскольку невозможно добавить другой сервер в том же домене.

  Можно включить VPN во время автоматического развертывания с помощью сценария Windows PowerShell , либо настроить его с помощью мастера настройки после начальной установки параметров.

  Чтобы включить VPN с помощью Windows PowerShell, выполните следующую команду с правами администратора на сервере под управлением Windows Server Essentials и введите все необходимые сведения.

```
##
## To configure external domain and SSL certificate (if not yet done in unattended Initial Configuration).
##

$myExternalDomainName = 'remote.contoso.com';   ## corresponds to A or AAAA DNS record(s) that can be resolved on Internet and routed to the server
$mySslCertificateFile = 'C:\ssl.pfx';   ## full path to SSL certificate file
$mySslCertificatePassword = ConvertTo-SecureString  œAsPlainText  œForce '******';   ## password for private key of the SSL certificate
$skipCertificateVerification = $true;   ## whether or not, skip verification for the SSL certificate

Set-WssDomainNameConfiguration  œDomainName $myExternalDomainName  œCertificatePath $mySslCertificateFile  œCertificateFilePassword $mySslCertificatePassword  œNoCertificateVerification
##
## To install VPN with static IPv4 pool (and allow all existing users to establish VPN).
##

Install-WssVpnServer -IPv4AddressRange ('192.168.0.160','192.168.0.240') -ApplyToExistingUsers;

```

> [!NOTE]
>  Если невозможно предоставить VPN-подключение до того как клиент получит права доступа к серверу, убедитесь в том, что порт сервера 3389 открыт для доступа через Интернет, чтобы клиент смог использовать протокол удаленного доступа к рабочему столу для подключения к серверу и его настройки.

##  <a name="customize-the-image-of-windows-server-essentials-experience-role"></a><a name="BKMK_CustomizeImage"></a> Настройка образа роли Windows Server Essentials
 Перед настройкой роли Windows Server Essentials Experience можно выполнить настройку ее образа. Дополнительные сведения о стандартном процессе Windows Server Sysprep см. в разделе [Комплект средств для развертывания и оценки Windows](/previous-versions/windows/hh825420(v=win.10)). После подготовки образа с помощью средства Sysprep можно его использовать или запаковать в файл Install.wim для последующего развертывания.

 При использовании диспетчера виртуальных машин можно создать шаблон на основе запущенного сервера. Для подготовки работающей копии используется Sysprep, который завершает работу компьютера. После сохранения шаблона в библиотеку можно использовать его при необходимости.

 После установки роли Windows Server Essentials можно настроить функции Windows Server Essentials. Одной из самых важных настроек является раздел реестра **IsHosted** : **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\Deployment\IsHosted**.

 Если этот раздел имеет значение 0x1, некоторые локальные компоненты изменят поведение системы. Такие изменения включают в себя следующее:

- **Архивация данных клиента**. По умолчанию архивация данных клиента отключена для вновь присоединившихся клиентских компьютеров.

- **Служба восстановления клиентских данных**. Служба восстановления клиентских данных будет отключена, а пользовательский интерфейс службы скрыт из панели мониторинга.

- **История файлов**. Настройки истории файлов для учетных записей новых пользователей не будут автоматически управляться сервером.

- **Архивация данных сервера**. Архивация данных сервера будет отключена, а пользовательский интерфейс службы будет скрыт из панели мониторинга.

- **Дисковые пространства**. Пользовательский интерфейс службы управления дисковыми пространствами будет скрыт из панели мониторинга.

- **Повсеместный доступ**. Установка параметров маршрутизатора и VPN будет по умолчанию пропущена при запуске мастера настройки повсеместного доступа.

  Если вам необходимо управлять поведением всех компонентов, вы можете установить для каждого из них соответствующий раздел реестра. Дополнительные сведения о настройке раздела реестра см. в разделе [Настройка и развертывание Windows Server Essentials в Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-8.1-and-8/dn293241(v=win.10)).

##  <a name="automate-the-deployment-of-windows-server-essentials-experience"></a><a name="BKMK_AutomateDeployment"></a> Автоматизируйте развертывание интерфейса Windows Server Essentials
 Чтобы автоматизировать развертывание, необходимо сначала развернуть операционную систему, а затем установить роль Windows Server Essentials Experience.

-   Чтобы автоматически развернуть Windows Server 2012 R2 Standard или Windows Server 2012 R2 Datacenter, следуйте инструкциям в [комплекте средств для развертывания и оценки Windows](/previous-versions/windows/hh825420(v=win.10)).

-   Сведения об установке роли Windows Server Essentials с помощью Windows PowerShell см. в статье [Установка и настройка Windows Server Essentials](/previous-versions/windows/it-pro/windows-server-essentials-sbs/dn281793(v=ws.11)).

> [!NOTE]
>  Убедитесь, что параметры часового пояса для виртуальной машины узла и интерфейса Windows Server Essentials совпадают. В противном случае могут возникнуть ошибки, К ним относятся: Начальная конфигурация сервера может не быть успешной в задачах, связанных с сертификатом. После установки роли Windows Server Essentials может не работать этот сертификат в течение нескольких часов, а сведения об устройстве будут обновлены неправильно.

 После развертывания необходимо использовать Windows PowerShell cmdlet **Get-WssConfigurationStatus**, чтобы проверить успешность начальной настройки. Должен вернуться один из следующих статусов: **Notstarted**, **FinishedWithWarning**, **Running**, **Finished**, **Failed**либо **PendingReboot**.

 Во время начальной настройки сервер будет перезапущен. Если необходимо предотвратить автоматический перезапуск сервера, перед запуском начальной настройки можно использовать следующую команду для добавления раздела реестра:

```
New-ItemProperty "HKLM:\Software\Microsoft\Windows Server\Setup"Ã‚Â  -Name "WaitForReboot" -Value 1 -PropertyType "DWord" -Force -Confirm:$false

```

 После запуска начальной настройки можно использовать **Get-WssConfigurationStatus** для проверки статуса начальной настройки; как только вы получите статус **PendingReboot**, можно перезапустить сервер.

##  <a name="migrate-data-from-windows-small-business-server-to-windows-server-essentials-experience"></a><a name="BKMK_Migrate"></a> Перенос данных из Windows Small Business Server в интерфейс Windows Server Essentials
 Можно выполнить миграцию данных с серверов под Windows Small Business Server 2011, Windows Small Business Server 2008, Windows Small Business Server 2003 или Windows Server Essentials на сервер под Windows Server Essentials. Ознакомьтесь с руководством по миграции перехода [на Windows Server Essentials](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md) для локальных 2migrations и внесите необходимые изменения на основе среды размещения.

> [!NOTE]
>  Рекомендуется размещать исходный сервер и сервер назначения в одной подсети. Если это невозможно, необходимо обеспечить выполнение следующих условий:
>
> - Исходный сервер и целевой сервер могут получить доступ ко всем остальным с внутренним DNS-именам.
>   -   Все необходимые порты должны быть открыты.

 После переноса данных можно обновить лицензию для снятия ограничений и блокировки. Дополнительные сведения см. [в статье переход с Windows Server Essentials на Windows server 2012 Standard](/previous-versions/windows/it-pro/windows-server-essentials-sbs/jj247582(v=ws.11)).

##  <a name="perform-common-tasks-by-using-windows-powershell"></a><a name="BKMK_PowerShell"></a> Выполнение общих задач с помощью Windows PowerShell
 В данном разделе описаны некоторые общие задачи, которые можно выполнять с помощью Windows PowerShell.

### <a name="enable-remote-web-access"></a>Подключение удаленного веб-доступа
 **Синтаксис**

 Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]

 **Пример**:

 $Enable Вссремотевебакцесс Œденякцессбидефаулт Œапплитоексистингусерс

 Данная команда позволяет включить удаленный веб-доступ с помощью автоматически настроенного маршрутизатора и изменить установленные по умолчанию права доступа для всех существующих пользователей.

### <a name="add-user"></a>Добавление пользователя
 **Синтаксис**

 Add-Вссусер [-name] <строка \> [-password] <SecureString \> [-AccessLevel <строка \> {пользователь &#124; Администратор}] [-FirstName <строка \> ] [-LastName <строка \> ] [-алловремотеакцесс] [-алловвпнакцесс] [<общиепараметры \> ]

 **Пример**:

 $password = ConvertTo-SecureString "Passw0rd!" -AsPlainText œфорце $ Add-Вссусер-Name User2Test-Password $password-AccessLevel администратор — FirstName Пользователь2-LastName Test

 Эта команда добавит администратора с именем User2Test с Password Passw0rd!.

### <a name="add-server-folder"></a>Добавление папки сервера
 **Синтаксис**

 Add-Вссфолдер [-name] <строка \> [-path] <строка \> [[-Description] <строка \> ] [-киппермиссионс] [<общиепараметры \> ]

 **Пример**:

 $Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"

 Эта команда добавляет папку сервера с именем Митестфолдер в указанном расположении.

##  <a name="email-integration-with-windows-server-essentials"></a><a name="BKMK_EmailIntegration"></a> Интеграция электронной почты с Windows Server Essentials
 Вы можете интегрировать интерфейс Windows Server Essentials с Microsoft 365 или размещенным сервером Exchange Server. Если требуется, чтобы клиент использовал услуги размещенной службы электронной почты, необходимо выполнить надстройку для интеграции Windows Server Essentials Experience с размещенной службой электронной почты. Дополнительные сведения см. в статье [Пакет SDK для Windows Server](/previous-versions/windows/server-essentials/gg513877(v=msdn.10)).

##  <a name="monitor-and-manage-by-using-native-tools"></a><a name="BKMK_Monitoring"></a> Мониторинг и управление с помощью собственных средств
 В этом разделе обсуждаются собственные средства, доступные в Windows Server 2012 R2 для мониторинга сервера и управления им.

### <a name="group-policy"></a>Групповая политика
  Опыт работы Windows Server Essentials использует встроенную поддержку групповая политика в Windows Server 2012 R2 и предоставляет пользовательский интерфейс для настройки параметров перенаправления папок и безопасности.

> [!NOTE]
>  Если в размещенной среде подключена функция переадресации папок для профиля пользователя, большой объем обрабатываемых данных может увеличить время вхождения на сервер для конечного пользователя.

### <a name="system-center-monitoring-pack"></a>Пакет мониторинга системного центра
 Пакет мониторинга System Center для интерфейса Windows Server Essentials наблюдает за системой предупреждений о работоспособности, помогающей управлять большим количеством серверов под управлением Windows Server Essentials, предназначенных для малых бизнес-организаций. Дополнительные сведения см. в статье [пакет управления System Center для Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809).

### <a name="backup-and-restore"></a>Резервное копирование и восстановление
  Windows Server 2012 R2 с интерфейсом Windows Server Essentials позволяет выполнять резервное копирование серверов и клиентских компьютеров в сети.

#### <a name="server-backup"></a>Архивация данных сервера
 Windows Server Essentials поддерживает два типа архивации сервера: локальную и удаленную. Если необходимо развернуть собственное решение архивации сервера, вы можете изменить настройки этих параметров.

-   **Локальная архивация** . Позволяет выполнить регулярную инкрементную архивацию на уровне блока на отдельный диск. В качестве поставщика услуг размещения вы можете подключить виртуальный жесткий диск к виртуальной машине под управлением Windows Server Essentials, а затем настроить архивацию сервера для этого виртуального жесткого диска. Виртуальный жесткий диск должен располагаться на физическом жестком диске, на котором не запущена виртуальная машина под управлением Windows Server Essentials.

    > [!NOTE]
    >  Если у вас имеются другие средства резервного копирования для виртуальных машин и вашим пользователям не требуется стандартная функция архивации данных сервера Windows Server Essentials, вы можете отключить ее и удалить соответствующий пользовательский интерфейс из панели мониторинга. Дополнительные сведения см. в подразделе [Настройка архивации сервера](/previous-versions/windows/it-pro/windows-8.1-and-8/dn293413(v=win.10)) раздела [Настройка и развертывание Windows Server Essentials в Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-8.1-and-8/dn293241(v=win.10)).

-   **Удаленная архивация** . Позволяет регулярно архивировать данные сервера через использование облачной службы. Вы можете скачать и установить модуль интеграции Microsoft Azure Backup для Windows Server Essentials, чтобы использовать Azure Backup, предоставляемый корпорацией Майкрософт.

     Дополнительные сведения см. в разделе Интеграция Windows Azure Backup с Windows Server Essentials статьи [Управление резервным копированием сервера](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md).

     Если вы или ваши пользователи пользуются службами других поставщиков облачных услуг, необходимо выполнить следующие действия:

    -   Обновите пользовательский интерфейс панели мониторинга, чтобы он был связан с предпочтительной облачной службой, а не с Azure Backup по умолчанию.

    -   (Необязательно.) Разработать надстройку для панели мониторинга, необходимую для настройки облачной службы архивации и управления ею.

#### <a name="client-computer-backup"></a>Архивация клиентских компьютеров
 Windows Server Essentials Experience поддерживает два вида архивации данных компьютера клиента: полная архивация данных и история файлов.

> [!NOTE]
>  Архивация данных клиента может повлиять на работоспособность системы, поскольку данные клиента передаются на сервер через VPN.

##### <a name="full-client-backup"></a>Полная архивация данных клиента
 Полная архивация данных включена по умолчанию для всех клиентских устройств, подключенных к сети Windows Server Essentials. Этот вид архивации выполняет полное резервное копирование информации и данных клиента и поддерживает дедупликацию данных. Данные резервной копии будут храниться на сервере, работающем под Windows Server Essentials. Это позволяет клиенту восстановить данные из предыдущей точки восстановления при возникновении сбоя в системе.

 Ниже представлена некоторая важная информация касательно полной архивации данных клиентского компьютера:

-   **Производительность** Начальная Архивация клиента может занять много времени из-за объема отправляемых данных.

-   **Стабильность работы** Иногда подключение к Интернету не является стабильным на стороне клиента. Резервное копирование клиента разработано для автоматического возобновления, а резервная копия базы данных клиента создает контрольную точку при каждом резервном копировании 40 ГБ данных. Это значение можно уменьшить, если подключение к Интернету нестабильно.

    -   Чтобы включить задание контрольной точки: на сервере задайте для раздела реестра **HKLM\Software\Microsoft\Windows сервер\баккуп\жетчеккпоинтжобс** значение 1.

    -   Изменение порогового значения контрольной точки На клиентском компьютере измените значение **HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold** со значения по умолчанию в 40 ГБ.

-   **Восстановление исходного состояния клиентского компьютера** . Поскольку среда предустановки Windows не поддерживает VPN-подключение, восстановление исходного состояния клиентского компьютера невозможно. Чтобы скрыть задачу "Служба восстановления клиента", выполните действия, описанные в разделе [Настройка и развертывание Windows Server Essentials в Windows server 2012 R2](/previous-versions/windows/it-pro/windows-8.1-and-8/dn293241(v=win.10)).

##### <a name="file-history"></a>История файлов
 История файлов — это функция ОС Windows 8.1 и Windows 8, позволяющая архивировать данные профиля (библиотеки, рабочий стол, контакты, избранное) в общую сетевую папку. Можно централизованно управлять параметрами истории файлов всех компьютеров под управлением Windows 8.1 или Windows 8, подключенных к сети Windows Server Essentials. Данные архивации хранятся на сервере под управлением Windows Server Essentials. Для скрытия задачи службы восстановления данных клиента необходимо выполнить действия, описанные в разделе [Настройка и развертывание Windows Server Essentials на Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-8.1-and-8/dn293241(v=win.10)).

### <a name="storage-management"></a>Управление хранением
 Дисковые пространства позволяют объединить физический объем памяти разрозненных жестких дисков, динамически добавлять жесткие диски и создавать тома данных с заданными уровнями устойчивости. Можно выполнять это на ведущем узле или на виртуальной машине. Если вы хотите скрыть этот компонент в виртуальной машине под управлением Windows Server Essentials, следуйте инструкциям в разделе [Настройка и развертывание Windows Server Essentials в Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-8.1-and-8/dn293241(v=win.10)).

##  <a name="test-scenarios"></a><a name="BKMK_Scenarios"></a> Сценарии тестирования
 Для успешного размещения рекомендуется провести проверку следующих сценариев:


-   [Развертывание сервера](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerDeploy)

-   [Конфигурация сервера](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerConfig2)

-   [Управление сервером](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerManage)

-   [Взаимодействие с клиентом](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ClientXP)


###  <a name="server-deployment"></a><a name="BKMK_ServerDeploy"></a> Развертывание сервера
 Можно проверить следующие сценарии развертывания сервера:

-   Разверните сервер под Windows Server 2012 R2 в качестве контроллера домена в лабораторной среде, а затем установите роль Windows Server Essentials Experience.

-   Разверните сервер под Windows Server 2012 R2 в лабораторной среде, присоедините этот сервер к существующему домену, а затем установите роль Windows Server Essentials Experience.

-   Настройка образа Windows Server Essentials при необходимости.

-   Автоматизация развертывания Windows Server Essentials с помощью файла установки и Windows PowerShell.

-   Миграция локальных серверов под управлением Windows Small Business Server на размещенные сервера под управлением Windows Server Essentials.

###  <a name="server-configuration"></a><a name="BKMK_ServerConfig2"></a> Конфигурация сервера
 Можно проверить следующие сценарии конфигурации сервера:

-   Настройте повсеместный доступ (к виртуальной частной сети, удаленный веб-доступ и DirectAccess).

-   Настройте хранилище и папки сервера.

-   Включите BranchCache.

-   (Если применимо.) Настройте параметры архивации сервера, веб-архивации, архивации данных клиента и истории файлов.

-   (Если применимо.) Настройте и управляйте дисковыми пространствами.

-   (Если применимо) Настройка интеграции решения электронной почты (Microsoft 365 и размещенного сервера Exchange Server).

-   (Если применимо.) Настройте интеграции с другими интернет-службами Майкрософт.

-   (Если применимо) настройте сервер мультимедиа.

###  <a name="server-management"></a><a name="BKMK_ServerManage"></a> Управление сервером
 Можно проверить следующие сценарии конфигурации сервера:

-   Управление пользователями и группами.

-   Настройте и получайте электронные уведомления для оповещений.

-   Запустите анализатор соответствия рекомендациям и убедитесь в отсутствии ошибок и предупреждений.

-   Настройте пакет управления системным центром.

-   Настройте функцию восстановления сервера в случае сбоя в операционной системе.

###  <a name="client-experience"></a><a name="BKMK_ClientXP"></a> Взаимодействие с клиентом
 Можно проверить следующие сценарии взаимодействия с конечным пользователем:

-   Развертывание клиентских компьютеров через Интернет (ПК или Mac).

-   Использование панели запуска на клиентском компьютере для доступа к общим папкам.

-   Доступ к ресурсам сервера через службу удаленного доступа с помощью различных устройств (ПК, телефон, планшет).

-   Доступ к приложению "Мой сервер" для Windows Phone.

-   (Если применимо.) Доступ к истории файлов, архивации и восстановлению данных клиента, переадресации папок.

-   (Если применимо.) Проверка интеграции служб электронной почты.

##  <a name="support-information"></a><a name="BKMK_Support"></a> Сведения о поддержке
 Вы можете скачать пакет средств разработки программного обеспечения (SDK) Windows Server Essentials и комплект средств для развертывания и оценки Windows Server Essentials (ADK):

-   [Пакет средств разработки программного обеспечения Windows Server Essentials](/previous-versions/windows/server-essentials/gg513877(v=msdn.10)) Tool

-   [Настройка и развертывание Windows Server Essentials в Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-8.1-and-8/dn293241(v=win.10))

## <a name="additional-references"></a>Дополнительные ссылки

-   [Что нового в Windows Server Essentials](../get-started/what-s-new.md)

-   [Установка Windows Server Essentials](Install-Windows-Server-Essentials.md)

-   [Начало работы с Windows Server Essentials](../get-started/get-started.md)