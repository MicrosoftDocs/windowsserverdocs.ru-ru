---
title: Настройка подключений постоянно подключенного VPN-профиля клиента Windows 10
description: На этом шаге вы узнаете о параметрах и схеме Профилексмл, а также о настройке клиентских компьютеров Windows 10 для связи с этой инфраструктурой с помощью VPN-подключения.
ms.topic: article
ms.date: 05/29/2018
ms.assetid: d165822d-b65c-40a2-b440-af495ad22f42
ms.localizationpriority: medium
ms.author: v-tea
author: Teresa-MOTIV
ms.reviewer: deverette
ms.openlocfilehash: c1f97ae4ec0ef39db2f0924bf2b6c3884f6ea1a9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946757"
---
# <a name="step-6-configure-windows-10-client-always-on-vpn-connections"></a>Шаг 6. Настройка клиента Windows 10 Always On VPN-подключений

>Область применения: Windows Server (половина ежегодного канала), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Назад:** Шаг 5. Настройка параметров DNS и брандмауэра](vpn-deploy-dns-firewall.md)<br>
- [**Далее:** Шаг 7. Используемых Условный доступ для VPN-подключений с помощью Azure AD](../../ad-ca-vpn-connectivity-windows10.md)

На этом шаге вы узнаете о параметрах и схеме Профилексмл, а также о настройке клиентских компьютеров Windows 10 для связи с этой инфраструктурой с помощью VPN-подключения.

VPN-клиент Always On можно настроить с помощью PowerShell, Microsoft Endpoint Configuration Manager или Intune. Для всех трех требуется профиль VPN в формате XML, чтобы настроить соответствующие параметры VPN. Автоматизация регистрации PowerShell для организаций без Configuration Manager или Intune невозможна.

>[!NOTE]
>Групповая политика не включает административные шаблоны для настройки VPN-клиента Windows 10 Always On Remote Access.  Однако можно использовать сценарии входа в систему.

## <a name="profilexml-overview"></a>Обзор Профилексмл

Профилексмл — это узел URI в поставщике служб шифрования поддержка vpnv2. Вместо настройки каждого узла поддержка vpnv2 CSP по отдельности, например триггеров, списков маршрутов и протоколов проверки подлинности, этот узел используется для настройки VPN-клиента Windows 10 путем доставки всех параметров как одного блока XML на один узел CSP. Схема Профилексмл сопоставляет схему узлов CSP поддержка vpnv2 почти одинаково, но некоторые термины немного отличаются.

Профилексмл используется во всех методах доставки, описанных в этом развертывании, включая Windows PowerShell, Microsoft Endpoint Configuration Manager и Intune. Существует два способа настройки узла Профилексмл поддержка vpnv2 CSP в этом развертывании:

- **OMA-DM**. Один из способов — использовать поставщик MDM с использованием OMA-DM, как описано выше в разделе [Поддержка VPNV2 CSP Nodes](../always-on-vpn-technology-overview.md#vpnv2-csp-nodes). С помощью этого метода можно легко вставить XML-разметку конфигурации профиля VPN в узел Профилексмл CSP при использовании Intune.

- **Инструментарий управления Windows (WMI) (WMI) для моста CSP**. Второй способ настройки узла CSP Профилексмл — использование моста WMI-to-CSP — класс WMI с именем **MDM_VPNv2_01**, который имеет доступ к поддержка vpnv2 CSP и узлу профилексмл. При создании нового экземпляра класса WMI Инструментарий WMI использует CSP для создания профиля VPN при использовании Windows PowerShell и Configuration Manager.

Несмотря на то что эти методы конфигурации различаются, для обоих требуется правильно отформатированный профиль VPN в формате XML. Чтобы использовать параметр Профилексмл поддержка vpnv2 CSP, создайте XML-файл с помощью схемы Профилексмл, чтобы настроить теги, необходимые для простого сценария развертывания. Дополнительные сведения см. в разделе [ПРОФИЛЕКСМЛ XSD](/windows/client-management/mdm/vpnv2-profile-xsd).

Ниже вы найдете все необходимые параметры и соответствующий тег Профилексмл. Каждый параметр настраивается в определенном теге в схеме Профилексмл, а не все из них находятся в собственном профиле. Дополнительные сведения о размещении тегов см. в схеме Профилексмл.

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

**Тип подключения:** Собственная IKEv2

Элемент Профилексмл:

```xml
<NativeProtocolType>IKEv2</NativeProtocolType>
```

**Маршрутизация:** Раздельное туннелирование

Элемент Профилексмл:

```xml
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>
```

**Разрешение имен:** Список сведений о доменных именах и DNS-суффикс

Элементы Профилексмл:

```xml
<DomainNameInformation>
<DomainName>.corp.contoso.com</DomainName>
<DnsServers>10.10.1.10,10.10.1.50</DnsServers>
</DomainNameInformation>

<DnsSuffix>corp.contoso.com</DnsSuffix>
```

**Активация:** Always On и обнаружение доверенных сетей

Элементы Профилексмл:

```xml
<AlwaysOn>true</AlwaysOn>
<TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>
```

**Проверка подлинности:** PEAP-TLS с сертификатами пользователей, защищенными доверенным платформенным модулем

Элементы Профилексмл:

```xml
<Authentication>
<UserMethod>Eap</UserMethod>
<Eap>
<Configuration>...</Configuration>
</Eap>
</Authentication>
```

Для настройки некоторых механизмов проверки подлинности VPN можно использовать простые теги. Тем не менее, протоколы EAP и PEAP более сложны. Самый простой способ создать XML-разметку — настроить VPN-клиент с помощью его параметров EAP, а затем экспортировать эту конфигурацию в XML.

Дополнительные сведения о параметрах EAP см. в разделе [конфигурация EAP](/windows/client-management/mdm/eap-configuration).

## <a name="manually-create-a-template-connection-profile"></a>Создание профиля подключения шаблона вручную

На этом шаге используется защищенный протокол PEAP для защиты обмена данными между клиентом и сервером. В отличие от простого имени пользователя и пароля, для работы этого подключения требуется уникальный раздел Еапконфигуратион в профиле VPN.

Вместо описания способа создания XML-разметки с нуля с помощью параметров в Windows можно создать шаблон профиля VPN. После создания шаблона VPN-профиля вы используете Windows PowerShell для использования части Еапконфигуратион из этого шаблона для создания окончательной Профилексмл, развертываемого позже в развертывании.

### <a name="record-nps-certificate-settings"></a>Запись параметров сертификата NPS

Перед созданием шаблона Обратите внимание на имя узла или полное доменное имя (FQDN) сервера NPS из сертификата сервера и имени центра сертификации, который выдал сертификат.

**PROCEDURE**

1. На сервере NPS откройте сервер политики сети.

2. В консоли NPS в разделе политики щелкните **политики сети**.

3. Щелкните правой кнопкой мыши **подключения виртуальной частной сети (VPN)** и выберите пункт **свойства**.

4. Перейдите на вкладку **ограничения** и нажмите кнопку **методы проверки подлинности**.

5. В списке Типы EAP щелкните **Microsoft: Protected EAP (PEAP)** и нажмите кнопку **изменить**.

6. Запишите значения для **сертификата, выданного** и **издателем**.

    Эти значения используются в предстоящей конфигурации шаблона VPN. Например, если полное доменное имя сервера — nps01.corp.contoso.com, а имя узла — NPS01, то оно основывается на имени FQDN или DNS сервера, например nps01.corp.contoso.com.

7. Отмена диалогового окна Изменение свойств защищенного EAP.

8. Отмените диалоговое окно свойства подключений виртуальной частной сети (VPN).

9. Закройте сервер политики сети.

>[!NOTE]
>Если у вас несколько серверов NPS, выполните эти действия для каждого из них, чтобы профиль VPN мог проверить каждый из них.

### <a name="configure-the-template-vpn-profile-on-a-domain-joined-client-computer"></a>Настройка шаблона VPN-профиля на клиентском компьютере, присоединенном к домену

Теперь, когда у вас есть необходимые сведения, настройте профиль VPN шаблона на клиентском компьютере, присоединенном к домену. Тип используемой учетной записи пользователя (например, "Стандартный пользователь" или "Администратор") для этой части процесса не имеет значения.

Тем не менее, если вы не перезапустили компьютер после настройки автоматической регистрации сертификата, сделайте это перед настройкой VPN-подключения к шаблону, чтобы убедиться, что на нем есть пригодный для использования сертификат.

>[!NOTE]
>Невозможно вручную добавить дополнительные свойства VPN, такие как правила NRPT, Always On, обнаружение доверенных сетей и т. д. На следующем шаге создается тестовое VPN-подключение, которое проверяет конфигурацию VPN-сервера и возможность установить VPN-подключение к серверу.

**Создание отдельного тестового VPN-подключения вручную**

1.  Войдите на клиентский компьютер, присоединенный к домену, как член группы " **пользователи VPN** ".

2.  В меню Пуск введите **VPN**и нажмите клавишу ВВОД.

3.  В области сведений щелкните **Добавить VPN-подключение**.

4.  В списке Поставщик VPN выберите **Windows (встроенная)**.

5.  В окне имя подключения введите **template**.

6.  В поле имя или адрес сервера введите **внешнее** полное доменное имя VPN-сервера (например, **VPN.contoso.com**).

7.  Нажмите кнопку **Сохранить**.

8.  В разделе связанные параметры щелкните **изменить параметры адаптера**.

9.  Щелкните правой кнопкой мыши **шаблон**и выберите пункт **свойства**.

10. На вкладке **Безопасность** в **поле Тип VPN**щелкните **IKEv2**.

11. В меню Шифрование данных выберите пункт **Максимальная стойкость шифрования**.

12. Щелкните **использовать протокол расширенной проверки подлинности (EAP)**. затем в окне **использование протокола EAP**выберите **Microsoft: защищенный EAP (PEAP) (шифрование включено)**.

13. Щелкните **Свойства** , чтобы открыть диалоговое окно Свойства защищенного EAP, и выполните следующие действия.

    а. В поле **Подключение к этим серверам** введите имя сервера политики сети, полученное из параметров проверки подлинности сервера NPS, ранее в этом разделе (например, NPS01).

    >[!NOTE]
    >Введенное имя сервера должно совпадать с именем в сертификате. Это имя было восстановлено ранее в этом разделе. Если имя не совпадает, произойдет сбой подключения, в котором говорится, что "подключение было запрещено из-за политики, настроенной на сервере RAS/VPN".

    b.  В разделе Доверенные корневые центры сертификации выберите корневой ЦС, выдавший сертификат сервера политики сети (например, Contoso-CA).

    c.  В окне уведомления перед подключением щелкните **не спрашивать пользователя, чтобы авторизовать новые серверы или доверенные ЦС**.

    d.  В окне Выбор метода проверки подлинности щелкните **смарт-карта или иной сертификат**и нажмите кнопку **настроить**. Откроется диалоговое окно смарт-карта или свойства другого сертификата.

    д)  Щелкните **использовать сертификат на этом компьютере**.

    е)  В поле Подключение к этим серверам введите имя сервера NPS, полученное из параметров проверки подлинности сервера NPS на предыдущих шагах.

    ж.  В разделе Доверенные корневые центры сертификации выберите корневой ЦС, выдавший сертификат сервера NPS.

    h.  Установите флажок **не запрашивать пользователя авторизовать новые серверы или доверенные центры сертификации** .

    i.  Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно Свойства смарт-карты или другого сертификата.

    j.  Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно Свойства защищенного EAP.

14. Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно Свойства шаблона.

15. Закройте окно Сетевые подключения.

16. В окне параметры проверьте VPN, щелкнув **шаблон**, и нажмите кнопку **подключить**.

>[!IMPORTANT]
>Убедитесь, что VPN-подключение шаблона к VPN-серверу выполнено успешно. Это гарантирует правильность параметров EAP, прежде чем использовать их в следующем примере. Прежде чем продолжить, необходимо подключиться по крайней мере один раз. в противном случае профиль не будет содержать все сведения, необходимые для подключения к VPN.

## <a name="create-the-profilexml-configuration-files"></a>Создание файлов конфигурации Профилексмл

Перед выполнением этого раздела убедитесь, что создан и проверен шаблон VPN-подключение, которое описывается в разделе [Создание профиля подключения шаблона вручную](#manually-create-a-template-connection-profile) . Проверка VPN-подключения необходима, чтобы убедиться, что профиль содержит все сведения, необходимые для подключения к VPN.

Сценарий Windows PowerShell в листинге 1 создает на рабочем столе два файла, которые содержат теги **еапконфигуратион** на основе ранее созданного профиля подключения к шаблону:

- **VPN_Profile.xml.** Этот файл содержит XML-разметку, необходимую для настройки узла Профилексмл в CSP поддержка vpnv2. Используйте этот файл с службами MDM, совместимыми с OMA-DM, такими как Intune.

- **VPN_Profile.ps1.** Этот файл является сценарием Windows PowerShell, который можно запустить на клиентских компьютерах для настройки узла Профилексмл в поставщике служб шифрования поддержка vpnv2. Вы также можете настроить CSP, развернув этот скрипт с помощью Configuration Manager. Этот скрипт нельзя запустить в сеансе удаленный рабочий стол, включая расширенный сеанс Hyper-V.

>[!IMPORTANT]
>Для приведенных ниже примеров команд требуется Windows 10 Build 1607 или более поздней версии.

**Создание VPN_Profile.xml и VPN_Proflie.ps1**

1. Войдите на клиентский компьютер, присоединенный к домену, содержащий шаблон VPN-профиль с той же учетной записью пользователя, которую раздел создает с помощью [шаблона профиля подключения вручную](#manually-create-a-template-connection-profile) .

2. Вставьте листинг 1 в интегрированную среду сценариев Windows PowerShell (ISE) и настройте параметры, описанные в комментариях. Это $Template, $ProfileName, $Servers, $DnsSuffix, $DomainName, $TrustedNetwork и $DNSServers. Полное описание каждого параметра находится в комментариях.

3. Запустите сценарий, чтобы создать **VPN_Profile.xml** и **VPN_Profile.ps1** на рабочем столе.

#### <a name="listing-1-understanding-makeprofileps1"></a>Листинг 1. Основные сведения о MakeProfile.ps1

В этом разделе описывается пример кода, с помощью которого можно получить представление о том, как создать профиль VPN, специально для настройки Профилексмл в CSP поддержка vpnv2.

После сборки скрипта из этого примера кода и выполнения скрипта сценарий создает два файла: VPN_Profile.xml и VPN_Profile.ps1. Используйте VPN_Profile.xml, чтобы настроить Профилексмл в службах MDM, совместимых с OMA-DM, таких как Microsoft Intune.

Используйте сценарий **VPN_Profile.ps1** в Windows PowerShell или Configuration Manager конечной точки Майкрософт, чтобы настроить профилексмл на рабочем столе Windows 10.

>[!NOTE]
>Полный пример скрипта см. в разделе [MakeProfile.ps1 полный скрипт](#makeprofileps1-full-script).

##### <a name="parameters"></a>Параметры

Настройте следующие параметры:

**$Template**. Имя шаблона, из которого извлекается конфигурация EAP.

**$ProfileName**. Уникальный буквенно-цифровой идентификатор профиля. Имя профиля не должно содержать косую черту (/). Если имя профиля содержит пробел или другой символ, не являющийся буквенно-цифровым, он должен быть правильно экранирован в соответствии со стандартом кодировки URL-адреса.

**$Servers**. Общедоступный или маршрутизируемый IP-адрес или DNS-имя VPN-шлюза. Он может указывать на внешний IP-адрес шлюза или виртуальный IP-адрес для фермы серверов. Примеры, 208.147.66.130 или vpn.contoso.com.

**$DNSSuffix**. Указывает один или несколько разделенных запятыми DNS-суффиксов. Первая в списке также используется в качестве основного DNS-суффикса для подключения к интерфейсу VPN. Весь список также будет добавлен в Суффикссеарчлист.

**$DomainName**. Используется для указания пространства имен, к которому применяется политика. При выдаче запроса имени клиент DNS сравнивает имя в запросе со всеми пространствами имен в разделе Домаиннамеинформатионлист для поиска совпадения. Этот параметр может иметь один из следующих типов:

- FQDN — полное доменное имя
- Суффикс — суффикс домена, который будет добавлен к запросу ShortName для разрешения DNS. Чтобы указать суффикс, добавьте в начало точки (.) суффикс DNS.

**$DNSServers**. Список IP-адресов DNS-серверов с разделителями-запятыми для использования в пространстве имен.

**$TrustedNetwork**. Строка с разделителями-запятыми для обнаружения доверенной сети. VPN не подключается автоматически, когда пользователь находится в корпоративной беспроводной сети, где защищенные ресурсы напрямую доступны для устройства.

Ниже приведены примеры значений параметров, используемых в командах ниже. Убедитесь, что вы изменили эти значения для своей среды.

```xml
$TemplateName = 'Template'
$ProfileName = 'Contoso%20AlwaysOn%20VPN'
$Servers = 'vpn.contoso.com'
$DnsSuffix = 'corp.contoso.com'
$DomainName = '.corp.contoso.com'
$DNSServers = '10.10.0.2,10.10.0.3'
$TrustedNetwork = 'corp.contoso.com'
```

### <a name="prepare-and-create-the-profile-xml"></a>Подготовка и создание XML-файла профиля

В следующем примере команды получают параметры EAP из профиля шаблона.

```xml
$Connection = Get-VpnConnection -Name $TemplateName
if(!$Connection)
{
$Message = "Unable to get $TemplateName connection profile: $_"
Write-Host "$Message"
exit
}
$EAPSettings= $Connection.EapConfigXmlStream.InnerXml
```

### <a name="create-the-profile-xml"></a>Создание XML-файла профиля

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

```xml
$ProfileXML = @("
<VPNProfile>
  <DnsSuffix>$DnsSuffix</DnsSuffix>
  <NativeProfile>
<Servers>$Servers</Servers>
<NativeProtocolType>IKEv2</NativeProtocolType>
<Authentication>
  <UserMethod>Eap</UserMethod>
  <Eap>
    <Configuration>
     $EAPSettings
    </Configuration>
  </Eap>
</Authentication>
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>
  </NativeProfile>
  <AlwaysOn>true</AlwaysOn>
  <RememberCredentials>true</RememberCredentials>
  <TrustedNetworkDetection>$TrustedNetwork</TrustedNetworkDetection>
  <DomainNameInformation>
<DomainName>$DomainName</DomainName>
<DnsServers>$DNSServers</DnsServers>
</DomainNameInformation>
</VPNProfile>
")
```

### <a name="output-vpn_profilexml-for-intune"></a>Выходные VPN_Profile.xml Intune

Для сохранения XML-файла профиля можно использовать следующий пример команды:

```xml
$ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')
```

### <a name="output-vpn_profileps1-for-the-desktop-and-configuration-manager"></a>Вывод VPN_Profile.ps1 для настольных систем и Configuration Manager

В следующем примере кода выполняется настройка VPN-подключения AlwaysOn с помощью узла Профилексмл в поставщике служб шифрования поддержка vpnv2.

Этот сценарий можно использовать на рабочем столе Windows 10 или в Configuration Manager.

### <a name="define-key-vpn-profile-parameters"></a>Определение параметров профиля VPN-ключа

```xml
$Script = '$ProfileName = ''' + $ProfileName + ''''
$ProfileNameEscaped = $ProfileName -replace ' ', '%20'
```

### <a name="escape-special-characters-in-the-profile"></a>Экранирование специальных символов в профиле

```xml
$ProfileXML = $ProfileXML -replace '<', '&lt;'
$ProfileXML = $ProfileXML -replace '>', '&gt;'
$ProfileXML = $ProfileXML -replace '"', '&quot;'
```

### <a name="define-wmi-to-csp-bridge-properties"></a>Определение свойств моста WMI-CSP

```xml
$nodeCSPURI = "./Vendor/MSFT/VPNv2"
$namespaceName = "root\cimv2\mdm\dmmap"
$className = "MDM_VPNv2_01"
```

### <a name="determine-user-sid-for-vpn-profile"></a>Определите идентификатор безопасности пользователя для профиля VPN:

```xml
try
{
$username = Gwmi -Class Win32_ComputerSystem | select username
$objuser = New-Object System.Security.Principal.NTAccount($username.username)
$sid = $objuser.Translate([System.Security.Principal.SecurityIdentifier])
$SidValue = $sid.Value
$Message = "User SID is $SidValue."
Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to get user SID. User may be logged on over Remote Desktop: $_"
Write-Host "$Message"
exit
}
```

### <a name="define-wmi-session"></a>Определение сеанса WMI:

```xml
$session = New-CimSession
$options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
$options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
$options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)
```

### <a name="detect-and-delete-previous-vpn-profile"></a>Обнаружение и удаление предыдущего профиля VPN:

```xml
try
{
  $deleteInstances = $session.EnumerateInstances($namespaceName, $className, $options)
  foreach ($deleteInstance in $deleteInstances)
  {
    $InstanceId = $deleteInstance.InstanceID
    if ("$InstanceId" -eq "$ProfileNameEscaped")
    {
        $session.DeleteInstance($namespaceName, $deleteInstance, $options)
        $Message = "Removed $ProfileName profile $InstanceId"
        Write-Host "$Message"
    } else {
        $Message = "Ignoring existing VPN profile $InstanceId"
        Write-Host "$Message"
    }
  }
}
catch [Exception]
{
  $Message = "Unable to remove existing outdated instance(s) of $ProfileName profile: $_"
  Write-Host "$Message"
  exit
}
```

### <a name="create-the-vpn-profile"></a>Создайте профиль VPN:

```xml
try
{
  $newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", "String", "Key")
  $newInstance.CimInstanceProperties.Add($property)
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", "String", "Key")
  $newInstance.CimInstanceProperties.Add($property)
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", "String", "Property")
  $newInstance.CimInstanceProperties.Add($property)
  $session.CreateInstance($namespaceName, $newInstance, $options)
  $Message = "Created $ProfileName profile."


  Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to create $ProfileName profile: $_"
Write-Host "$Message"
exit
}

$Message = "Script Complete"
Write-Host "$Message"
```

### <a name="save-the-profile-xml-file"></a>Сохранение XML-файла профиля

```xml
$Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')

$Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
Write-Host "$Message"
```

## <a name="makeprofileps1-full-script"></a>MakeProfile.ps1 полный скрипт

В большинстве примеров для вставки Профилексмл в новый экземпляр класса MDM_VPNv2_01 WMI используется командлет Windows PowerShell Set-WmiInstance.

Однако это не работает в Configuration Manager, так как пакет нельзя запустить в контексте конечных пользователей. Таким образом, этот скрипт использует модель CIM для создания сеанса WMI в контексте пользователя, а затем создает в этом сеансе новый экземпляр класса WMI MDM_VPNv2_01. Этот класс WMI использует мост WMI-CSP для настройки CSP поддержка vpnv2. Поэтому, добавив экземпляр класса, вы настроите CSP.

>[!IMPORTANT]
>Для моста WMI в CSP требуются права локального администратора. Для развертывания профилей VPN каждого пользователя следует использовать Configuration Manager или MDM.

>[!NOTE]
>VPN_Profile.ps1 скриптов использует идентификатор безопасности текущего пользователя для обнаружения контекста пользователя. Так как в удаленный рабочий стол сеансе нет доступных идентификаторов безопасности, сценарий не работает в сеансе удаленный рабочий стол. Аналогично, он не работает в расширенном сеансе Hyper-V. Если вы тестируете удаленный доступ Always On VPN в виртуальных машинах, отключите расширенный сеанс на клиентских виртуальных машинах перед выполнением этого скрипта.

Следующий пример скрипта включает все примеры кода из предыдущих разделов. Убедитесь, что в примерах значений указаны значения, соответствующие вашей среде.

   ```makeProfile.ps1
    $TemplateName = 'Template'
    $ProfileName = 'Contoso AlwaysOn VPN'
    $Servers = 'vpn.contoso.com'
    $DnsSuffix = 'corp.contoso.com'
    $DomainName = '.corp.contoso.com'
    $DNSServers = '10.10.0.2,10.10.0.3'
    $TrustedNetwork = 'corp.contoso.com'


    $Connection = Get-VpnConnection -Name $TemplateName
    if(!$Connection)
    {
    $Message = "Unable to get $TemplateName connection profile: $_"
    Write-Host "$Message"
    exit
    }
    $EAPSettings= $Connection.EapConfigXmlStream.InnerXml

    $ProfileXML = @("
    <VPNProfile>
      <DnsSuffix>$DnsSuffix</DnsSuffix>
      <NativeProfile>
    <Servers>$Servers</Servers>
    <NativeProtocolType>IKEv2</NativeProtocolType>
    <Authentication>
      <UserMethod>Eap</UserMethod>
      <Eap>
       <Configuration>
        $EAPSettings
       </Configuration>
      </Eap>
    </Authentication>
    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>
      </NativeProfile>
    <AlwaysOn>true</AlwaysOn>
    <RememberCredentials>true</RememberCredentials>
    <TrustedNetworkDetection>$TrustedNetwork</TrustedNetworkDetection>
      <DomainNameInformation>
    <DomainName>$DomainName</DomainName>
    <DnsServers>$DNSServers</DnsServers>
    </DomainNameInformation>
    </VPNProfile>
    ")

    $ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')

     $Script = @("
      `$ProfileName = '$ProfileName'
      `$ProfileNameEscaped = `$ProfileName -replace ' ', '%20'

      `$ProfileXML = '$ProfileXML'

      `$ProfileXML = `$ProfileXML -replace '<', '&lt;'
      `$ProfileXML = `$ProfileXML -replace '>', '&gt;'
      `$ProfileXML = `$ProfileXML -replace '`"', '&quot;'

      `$nodeCSPURI = `"./Vendor/MSFT/VPNv2`"
      `$namespaceName = `"root\cimv2\mdm\dmmap`"
      `$className = `"MDM_VPNv2_01`"

      try
      {
      `$username = Gwmi -Class Win32_ComputerSystem | select username
      `$objuser = New-Object System.Security.Principal.NTAccount(`$username.username)
      `$sid = `$objuser.Translate([System.Security.Principal.SecurityIdentifier])
      `$SidValue = `$sid.Value
      `$Message = `"User SID is `$SidValue.`"
      Write-Host `"`$Message`"
      }
      catch [Exception]
      {
      `$Message = `"Unable to get user SID. User may be logged on over Remote Desktop: `$_`"
      Write-Host `"`$Message`"
      exit
      }

      `$session = New-CimSession
      `$options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
      `$options.SetCustomOption(`"PolicyPlatformContext_PrincipalContext_Type`", `"PolicyPlatform_UserContext`", `$false)
      `$options.SetCustomOption(`"PolicyPlatformContext_PrincipalContext_Id`", `"`$SidValue`", `$false)

      try
      {
     `$deleteInstances = `$session.EnumerateInstances(`$namespaceName, `$className, `$options)
     foreach (`$deleteInstance in `$deleteInstances)
     {
         `$InstanceId = `$deleteInstance.InstanceID
         if (`"`$InstanceId`" -eq `"`$ProfileNameEscaped`")
         {
             `$session.DeleteInstance(`$namespaceName, `$deleteInstance, `$options)
             `$Message = `"Removed `$ProfileName profile `$InstanceId`"
             Write-Host `"`$Message`"
         } else {
             `$Message = `"Ignoring existing VPN profile `$InstanceId`"
             Write-Host `"`$Message`"
         }
     }
      }
      catch [Exception]
      {
     `$Message = `"Unable to remove existing outdated instance(s) of `$ProfileName profile: `$_`"
     Write-Host `"`$Message`"
     exit
      }

      try
      {
     `$newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance `$className, `$namespaceName
     `$property = [Microsoft.Management.Infrastructure.CimProperty]::Create(`"ParentID`", `"`$nodeCSPURI`", `"String`", `"Key`")
     `$newInstance.CimInstanceProperties.Add(`$property)
     `$property = [Microsoft.Management.Infrastructure.CimProperty]::Create(`"InstanceID`", `"`$ProfileNameEscaped`", `"String`",      `"Key`")
     `$newInstance.CimInstanceProperties.Add(`$property)
     `$property = [Microsoft.Management.Infrastructure.CimProperty]::Create(`"ProfileXML`", `"`$ProfileXML`", `"String`", `"Property`")
     `$newInstance.CimInstanceProperties.Add(`$property)
     `$session.CreateInstance(`$namespaceName, `$newInstance, `$options)
     `$Message = `"Created `$ProfileName profile.`"

     Write-Host `"`$Message`"
      }
      catch [Exception]
      {
     `$Message = `"Unable to create `$ProfileName profile: `$_`"
     Write-Host `"`$Message`"
     exit
      }

      `$Message = `"Script Complete`"
      Write-Host `"`$Message`"
      ")

      $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')

    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"
   ```

## <a name="configure-the-vpn-client-by-using-windows-powershell"></a>Настройка VPN-клиента с помощью Windows PowerShell

Чтобы настроить CSP поддержка vpnv2 на клиентском компьютере с Windows 10, запустите VPN_Profile.ps1 сценарий Windows PowerShell, созданный в разделе [Создание XML-файла профиля](#create-the-profile-xml) . Откройте Windows PowerShell с правами администратора. в противном случае вы получите сообщение об ошибке " _отказано в доступе_".

После запуска VPN_Profile.ps1 для настройки профиля VPN можно в любой момент выполнить проверку, выполнив следующую команду в интегрированной среде сценариев Windows PowerShell:

```powershell
Get-WmiObject -Namespace root\cimv2\mdm\dmmap -Class MDM_VPNv2_01
```

**Успешные результаты командлета Get-WmiObject**

```powershell
__GENUS : 2
__CLASS : MDM_VPNv2_01
__SUPERCLASS:
__DYNASTY   : MDM_VPNv2_01
__RELPATH   : MDM_VPNv2_01.InstanceID="Contoso%20AlwaysOn%20VPN",ParentID
  ="./Vendor/MSFT/VPNv2"
__PROPERTY_COUNT: 10
__DERIVATION: {}
__SERVER: WIN01
__NAMESPACE : root\cimv2\mdm\dmmap
__PATH  : \\WIN01\root\cimv2\mdm\dmmap:MDM_VPNv2_01.InstanceID="Conto
  so%20AlwaysOn%20VPN",ParentID="./Vendor/MSFT/VPNv2"
AlwaysOn: True
ByPassForLocal  :
DnsSuffix   : corp.contoso.com
EdpModeId   :
InstanceID  : Contoso%20AlwaysOn%20VPN
LockDown:
ParentID: ./Vendor/MSFT/VPNv2
ProfileXML  : <VPNProfile><RememberCredentials>true</RememberCredentials>
  <AlwaysOn>true</AlwaysOn><DnsSuffix>corp.contoso.com</DnsSu
  ffix><TrustedNetworkDetection>corp.contoso.com</TrustedNetw
  orkDetection><NativeProfile><Servers>vpn.contoso.com;vpn.co
  ntoso.com</Servers><RoutingPolicyType>SplitTunnel</RoutingP
  olicyType><NativeProtocolType>Ikev2</NativeProtocolType><Au
  thentication><UserMethod>Eap</UserMethod><MachineMethod>Eap
  </MachineMethod><Eap><Configuration><EapHostConfig xmlns="h
  ttp://www.microsoft.com/provisioning/EapHostConfig"><EapMet
  hod><Type xmlns="https://www.microsoft.com/provisioning/EapC
  ommon">25</Type><VendorId xmlns="https://www.microsoft.com/p
  rovisioning/EapCommon">0</VendorId><VendorType xmlns="http:
  //www.microsoft.com/provisioning/EapCommon">0</VendorType><
  AuthorId xmlns="https://www.microsoft.com/provisioning/EapCo
  mmon">0</AuthorId></EapMethod><Config xmlns="https://www.mic
  rosoft.com/provisioning/EapHostConfig"><Eap xmlns="https://w
  ww.microsoft.com/provisioning/BaseEapConnectionPropertiesV1
  "><Type>25</Type><EapType xmlns="https://www.microsoft.com/p
  rovisioning/MsPeapConnectionPropertiesV1"><ServerValidation
  ><DisableUserPromptForServerValidation>true</DisableUserPro
  mptForServerValidation><ServerNames>NPS</ServerNames><Trust
  edRootCA>3f 07 88 e8 ac 00 32 e4 06 3f 30 f8 db 74 25 e1
  2e 5b 84 d1 </TrustedRootCA></ServerValidation><FastReconne
  ct>true</FastReconnect><InnerEapOptional>false</InnerEapOpt
  ional><Eap xmlns="https://www.microsoft.com/provisioning/Bas
  eEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="
  https://www.microsoft.com/provisioning/EapTlsConnectionPrope
  rtiesV1"><CredentialsSource><CertificateStore><SimpleCertSe
  lection>true</SimpleCertSelection></CertificateStore></Cred
  entialsSource><ServerValidation><DisableUserPromptForServer
  Validation>true</DisableUserPromptForServerValidation><Serv
  erNames>NPS</ServerNames><TrustedRootCA>3f 07 88 e8 ac 00
  32 e4 06 3f 30 f8 db 74 25 e1 2e 5b 84 d1 </TrustedRootCA><
  /ServerValidation><DifferentUsername>false</DifferentUserna
  me><PerformServerValidation xmlns="https://www.microsoft.com
  /provisioning/EapTlsConnectionPropertiesV2">true</PerformSe
  rverValidation><AcceptServerName xmlns="https://www.microsof
  t.com/provisioning/EapTlsConnectionPropertiesV2">true</Acce
  ptServerName></EapType></Eap><EnableQuarantineChecks>false<
  /EnableQuarantineChecks><RequireCryptoBinding>false</Requir
  eCryptoBinding><PeapExtensions><PerformServerValidation xml
  ns="https://www.microsoft.com/provisioning/MsPeapConnectionP
  ropertiesV2">true</PerformServerValidation><AcceptServerNam
  e xmlns="https://www.microsoft.com/provisioning/MsPeapConnec
  tionPropertiesV2">true</AcceptServerName></PeapExtensions><
  /EapType></Eap></Config></EapHostConfig></Configuration></E
  ap></Authentication></NativeProfile><DomainNameInformation>
  <DomainName>corp.contoso.com</DomainName><DnsServers>10.10.
      0.2,10.10.0.3</DnsServers><AutoTrigger>true</AutoTrigger></
  DomainNameInformation></VPNProfile>
RememberCredentials : True
TrustedNetworkDetection : corp.contoso.com
PSComputerName  : WIN01
```

Конфигурация Профилексмл должна быть правильно указана в структуре, орфографии, конфигурации и иногдам регистре букв. Если в структуре отображается что-то другое, то разметка Профилексмл, скорее всего, будет содержать ошибку.

Если необходимо устранить неполадки разметки, проще разместить ее в редакторе XML, чем устранять неполадки в интегрированной среде сценариев Windows PowerShell. В любом случае следует начать с самой простой версии профиля и добавить компоненты обратно в один момент времени, пока проблема не возникнет снова.

## <a name="configure-the-vpn-client-by-using-configuration-manager"></a>Настройка VPN-клиента с помощью Configuration Manager

В Configuration Manager можно развернуть профили VPN с помощью узла CSP Профилексмл, как и в Windows PowerShell. Здесь вы используете VPN_Profile.ps1 сценарий Windows PowerShell, созданный в разделе [Создание файлов конфигурации профилексмл](#create-the-profilexml-configuration-files).

Чтобы использовать Configuration Manager для развертывания профиля VPN удаленного доступа Always On на клиентских компьютерах Windows 10, необходимо сначала создать группу компьютеров или пользователей, которым вы развертываете профиль. В этом сценарии создайте группу пользователей для развертывания скрипта конфигурации.

### <a name="create-a-user-group"></a>Создание группы пользователей

1.  В консоли Configuration Manager откройте элемент активы и соответствие \\ коллекции пользователей.

2.  На вкладке **Главная** ленты в группе **создать** щелкните **создать коллекцию пользователей**.

3.  На странице Общие выполните следующие действия.

    а. В списке **имя**введите **VPN-пользователи**.

    b. Нажмите кнопку **Обзор**, выберите **все пользователи** и нажмите кнопку **ОК**.

    c. Щелкните **Далее**.

4.  На странице правила членства выполните следующие действия.

    а.  В **правилах членства**нажмите кнопку **Добавить правило**и выберите пункт **прямое правило**. В этом примере вы добавляете отдельных пользователей в коллекцию пользователей. Однако вы можете использовать правило запроса для динамического добавления пользователей в эту коллекцию для крупномасштабного развертывания.

    b.  На странице **приветствия** нажмите кнопку **Далее**.

    c.  На странице Поиск ресурсов в поле **значение**введите имя пользователя, которого нужно добавить. Имя ресурса включает домен пользователя. Чтобы включить результаты на основе частичного совпадения, вставьте **%** символ в конце условия поиска. Например, чтобы найти всех пользователей, содержащих строку "Лори", введите **% Лори%**. Щелкните **Далее**.

    d.  На странице Выбор ресурсов выберите пользователей, которых нужно добавить в группу, и нажмите кнопку **Далее**.

    д)  На странице Сводка нажмите кнопку **Далее**.

    е)  На странице завершения нажмите кнопку **Закрыть**.

6.  Вернитесь на страницу правила членства в мастере создания коллекции пользователей и нажмите кнопку **Далее**.

7.  На странице Сводка нажмите кнопку **Далее**.

8.  На странице завершения нажмите кнопку **Закрыть**.

После создания группы пользователей для получения профиля VPN можно создать пакет и программу для развертывания скрипта конфигурации Windows PowerShell, созданного в разделе [Создание файлов конфигурации профилексмл](#create-the-profilexml-configuration-files).

### <a name="create-a-package-containing-the-profilexml-configuration-script"></a>Создание пакета, содержащего скрипт конфигурации Профилексмл

1.  Разместите VPN_Profile.ps1 сценария в общей сетевой папке, к которой может получить доступ учетная запись компьютера сервера сайта.

2.  В консоли Configuration Manager откройте **Библиотека программного обеспечения \\ Управление приложениями \\ пакеты**.

3.  На вкладке **Главная** ленты в группе **создать** щелкните **создать пакет** , чтобы запустить мастер создания пакетов и программ.

4.  На странице пакет выполните следующие действия.

    а. В списке **имя**введите **Windows 10 Always on профиль VPN**.

    b. Установите флажок **Этот пакет содержит исходные файлы** и нажмите кнопку **Обзор**.

    c. В диалоговом окне задать исходную папку нажмите кнопку **Обзор**, выберите общую папку, содержащую VPN_Profile.ps1, и нажмите кнопку **ОК**.
        Убедитесь, что выбран сетевой путь, а не локальный путь. Иными словами, путь должен быть примерно таким, как * \\ файлового сервера \\ впнскрипт*, а не *c: \\ впнскрипт*.

1.  Щелкните **Далее**.

2.  На странице Тип программы нажмите кнопку **Далее**.

3.  На странице Стандартная программа выполните следующие действия.

    а.  В списке **имя**введите **сценарий профиля VPN**.

    b.  В **командной строке**введите **PowerShell.exe-ExecutionPolicy обход-файл "VPN_Profile.ps1"**.

    c.  В **режиме выполнения**щелкните **Запуск с правами администратора**.

    d.  Щелкните **Далее**.

4.  На странице требования выполните следующие действия.

    а.  Выберите **Эта программа может запускаться только на указанных платформах**.

    b.  Установите флажки **все Windows 10 (32-bit)** и **все windows 10 (64-bit)** .

    c.  В поле " **предполагаемое место на диске**" введите **1**.

    d.  В списке **максимально допустимое время выполнения (в минутах)** введите **15**.

    д)  Щелкните **Далее**.

5.  На странице Сводка нажмите кнопку **Далее**.

6.  На странице завершения нажмите кнопку **Закрыть**.

После создания пакета и программы необходимо развернуть его в группе " **пользователи VPN** ".

### <a name="deploy-the-profilexml-configuration-script"></a>Развертывание скрипта конфигурации Профилексмл

1.  В консоли Configuration Manager откройте библиотека программного обеспечения \\ Управление приложениями \\ пакеты.

2.  В окне **пакеты**щелкните **профиль VPN Windows 10 Always on**.

3.  На вкладке **программы** в нижней части области сведений щелкните правой кнопкой мыши элемент **Скрипт профиля VPN**, выберите пункт **Свойства**и выполните следующие действия.

    а.  На вкладке **Дополнительно** в поле **когда эта программа назначена компьютеру**выберите **один раз для каждого пользователя, который входит**в систему.

    b.  Нажмите кнопку **ОК**.

4.  Щелкните правой кнопкой мыши **сценарий профиля VPN** и выберите **развернуть** , чтобы запустить мастер развертывания программного обеспечения.

5.  На странице Общие выполните следующие действия.

    а.  Рядом с элементом **коллекция**нажмите кнопку **Обзор**.

    b.  В списке **типы коллекций** (вверху слева) щелкните **коллекции пользователей**.

    c.  Щелкните **VPN-пользователи**и нажмите кнопку **ОК**.

    d.  Щелкните **Далее**.

6.  На странице содержимое выполните следующие действия.

    а.  Нажмите кнопку **Добавить**и выберите **пункт точка распространения**.

    b.  В списке **Доступные точки распространения**выберите точки распространения, для которых требуется распространить скрипт конфигурации профилексмл, и нажмите кнопку **ОК**.

    c.  Щелкните **Далее**.

7.  На странице Параметры развертывания нажмите кнопку **Далее**.

8.  На странице Расписание выполните следующие действия.

    а.  Нажмите кнопку **создать** , чтобы открыть диалоговое окно Расписание назначений.

    b.  Щелкните **назначить немедленно после этого события**и нажмите кнопку **ОК**.

    c.  Щелкните **Далее**.

9.  На странице взаимодействие с пользователем выполните следующие действия.

    1.  Установите флажок **Установка программного обеспечения** .

    2.  Щелкните **Сводка**.

10. На странице Сводка нажмите кнопку **Далее**.

11. На странице завершения нажмите кнопку **Закрыть**.

Развернув скрипт конфигурации Профилексмл, войдите на клиентский компьютер Windows 10 с учетной записью пользователя, выбранной при создании коллекции пользователей. Проверьте конфигурацию VPN-клиента.

>[!NOTE]
>VPN_Profile.ps1 скриптов не работает в сеансе удаленный рабочий стол. Аналогично, он не работает в расширенном сеансе Hyper-V. Если вы тестируете удаленный доступ Always On VPN в виртуальных машинах, отключите расширенный сеанс на клиентских виртуальных машинах, прежде чем продолжить.

### <a name="verify-the-configuration-of-the-vpn-client"></a>Проверка конфигурации VPN-клиента

1.  На панели управления в разделе ** \\ безопасность системы**щелкните **Configuration Manager**.

2.  В диалоговом окне Свойства Configuration Manager на вкладке **действия** выполните следующие действия.

    а.  Щелкните **цикл оценки & получения политики компьютера**, щелкните **Запустить сейчас**и нажмите кнопку **ОК**.

    b.  Щелкните **цикл оценки & получения политики пользователя**, щелкните **Запустить сейчас**и нажмите кнопку **ОК**.

    c.  Нажмите кнопку **ОК**.

3.  Закройте панель управления.

Вскоре вы увидите новый профиль VPN.

## <a name="configure-the-vpn-client-by-using-intune"></a>Настройка VPN-клиента с помощью Intune

Чтобы использовать Intune для развертывания профилей VPN для удаленного доступа Windows 10 Always On, можно настроить узел CSP Профилексмл с помощью профиля VPN, созданного в разделе [Создание файлов конфигурации профилексмл](#create-the-profilexml-configuration-files), или можно использовать базовый пример кода EAP XML, приведенный ниже.

>[!NOTE]
>Теперь Intune использует группы Azure AD. Если Azure AD Connect синхронизирует группу "пользователи VPN" из локальной среды в Azure AD, а пользователи назначены группе "пользователи VPN", вы можете продолжать работу.

Создайте политику конфигурации VPN-устройства, чтобы настроить клиентские компьютеры Windows 10 для всех пользователей, добавленных в группу. Так как шаблон Intune предоставляет параметры VPN, скопируйте только \<EapHostConfig> \</EapHostConfig> часть файла VPN_ProfileXML.

### <a name="create-the-always-on-vpn-configuration-policy"></a>Создание Always On политики конфигурации VPN

1.    Войдите на [портал Azure](https://portal.azure.com/).

2.    Перейдите к **Intune**разделу  >  **профили конфигурации устройств**Intune  >  **Profiles**.

3.    Щелкните **создать профиль** , чтобы запустить мастер создания профиля.

4.    Введите **имя** для профиля VPN и (необязательно) описание.

1.   В разделе **платформа**выберите **Windows 10 или более поздней версии**и в раскрывающемся списке Тип профиля выберите **VPN** .

     >[!TIP]
     >Если вы создаете настраиваемую Профилексмл VPN, см. инструкции в статье [применение профилексмл с помощью Intune](/windows/security/identity-protection/vpn/vpn-profile-options#apply-profilexml-using-intune) .

2. На вкладке **Базовая VPN** проверьте или задайте следующие параметры.

    - **Имя подключения:** Введите имя VPN-подключения, которое отображается на клиентском компьютере на вкладке **VPN** в разделе **Параметры**, например _contoso аутовпн_.

    - **Серверы:** Добавьте один или несколько VPN-серверов, нажав кнопку **Добавить.**

    - **Описание** и **IP-адрес или полное доменное имя:** введите описание и IP-адрес или полное доменное имя VPN-сервера. Эти значения должны быть согласованы с именем субъекта в сертификате проверки подлинности VPN-сервера.

    - **Сервер по умолчанию:** Если это VPN-сервер по умолчанию, установите значение **true**. Это позволит использовать этот сервер в качестве сервера по умолчанию, используемого устройствами для установления соединения.

    - **Тип подключения:** Задайте для параметра значение **IKEv2**.

    - **Always On:** Задайте для параметра **Разрешить** автоматическое подключение к VPN при входе и подключение до тех пор, пока пользователь не отключится вручную.

    - **Запоминать учетные данные при каждом входе в систему**: логическое значение (true или false) для кэширования учетных данных. Если задано значение true, учетные данные кэшируются везде, где это возможно.

3.  Скопируйте следующую XML-строку в текстовый редактор:

    [!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]


    ```XML
    <EapHostConfig xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</AcceptServerName></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</AcceptServerName></PeapExtensions></EapType></Eap></Config></EapHostConfig>
    ```

4.  Замените ** \<TrustedRootCA> 5A 89 Fe cb 5b 49 A7 0b 1A 52 63 B7 35 ee D7 1c C2 68 4b<\/ трустедрутка>** в примере на отпечаток сертификата локального корневого центра сертификации в обоих местах.

    >[!Important]
    >Не используйте образец отпечатка в \<TrustedRootCA> \</TrustedRootCA> разделе ниже.  Трустедрутка должен быть отпечаткой сертификата локального корневого центра сертификации, который выдал сертификат проверки подлинности сервера для серверов RRAS и NPS. **Это не должен быть корневой сертификат облака или отпечаток промежуточного сертификата ЦС**.

5.  Замените ** \<ServerNames> NPS.contoso.com \</ServerNames> ** в образце XML полным доменным именем присоединенного к домену сервера политики сети, в котором выполняется проверка подлинности.

6.  Скопируйте измененную строку XML и вставьте ее в поле **EAP XML** (базовая VPN) и нажмите кнопку **ОК**.
    Политика конфигурации VPN-устройства Always On с использованием протокола EAP создается в Intune.


### <a name="sync-the-always-on-vpn-configuration-policy-with-intune"></a>Синхронизация политики конфигурации VPN Always On с Intune

Чтобы проверить политику конфигурации, войдите на клиентский компьютер с Windows 10 в качестве пользователя, добавленного в группу **Always on VPN-пользователи** , а затем выполните синхронизацию с Intune.

1.  В меню Пуск щелкните **Параметры**.

2.  В окне Параметры щелкните **учетные записи**и выберите **доступ к рабочей или учебной работе**.

3.  Щелкните профиль MDM и нажмите кнопку **сведения**.

4.  Нажмите кнопку **синхронизировать** , чтобы принудительно выполнить оценку и получение политики Intune.

5.  Закройте параметры. После синхронизации вы увидите, что профиль VPN доступен на компьютере.

## <a name="next-steps"></a>Дальнейшие действия

Развертывание Always On VPN завершено.  Другие возможности, которые можно настроить, см. в следующей таблице:

|Цель...  |Затем см...  |
|---------|---------|
|Настройка условного доступа для VPN    |[Шаг 7. Используемых Настройка условного доступа для VPN-подключения с помощью Azure AD](../../ad-ca-vpn-connectivity-windows10.md). на этом этапе можно точно настроить доступ VPN-пользователей с правами доступа к ресурсам с помощью [Azure Active Directory (Azure AD) условного доступа](/azure/active-directory/active-directory-conditional-access-azure-portal). Условный доступ Azure AD для подключения к виртуальной частной сети (VPN) поможет защитить VPN-подключения. Условный доступ — это модуль оценки на основе политик, который позволяет создавать правила доступа для любого приложения, подключенного к Azure Active Directory (Azure AD).         |
|Дополнительные сведения о дополнительных возможностях VPN  |[Дополнительные функции VPN](always-on-vpn-adv-options.md#advanced-vpn-features). на этой странице приводятся рекомендации по включению фильтров трафика VPN, настройке АВТОМАТИЧЕСКИх VPN-подключений с помощью триггеров приложений и настройке NPS для разрешения VPN-подключений только от клиентов, использующих сертификаты, выданные Azure AD.        |
