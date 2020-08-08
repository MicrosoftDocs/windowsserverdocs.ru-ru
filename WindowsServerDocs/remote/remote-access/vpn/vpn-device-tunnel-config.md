---
title: Настройка туннеля VPN-устройства в Windows 10
description: Узнайте, как создать туннель VPN-устройства в Windows 10.
ms.date: 11/05/2018
ms.topic: article
ms.assetid: 158b7a62-2c52-448b-9467-c00d5018f65b
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.openlocfilehash: 04500e2a9d5623aa9ce9796088bda2e4a6a5eccd
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996791"
---
# <a name="configure-vpn-device-tunnels-in-windows-10"></a>Настройка туннелей VPN-устройств в Windows 10

>Область применения: Windows 10 версии 1709

Always On VPN предоставляет возможность создания выделенного профиля VPN для устройства или компьютера. Always On VPN-подключения включают два типа туннелей:

- _Туннель устройства_ подключается к указанным VPN-серверам, прежде чем пользователи смогут войти на устройство. Сценарии подключения до входа в систему и в целях управления устройствами используют туннель устройства.

- _Туннель пользователя_ подключается только после входа пользователя на устройство. Пользовательский туннель позволяет пользователям получать доступ к ресурсам Организации через VPN-серверы.

В отличие от _пользовательского туннеля_, которое подключается только после входа пользователя на устройство или компьютер, _туннель устройства_ позволяет VPN устанавливать подключение до входа пользователя в систему. Туннель _туннеля устройства_ и _пользователь_ взаимодействуют независимо с их профилями VPN. они могут быть подключены одновременно и могут использовать разные методы проверки подлинности и другие параметры конфигурации VPN. Туннель пользователя поддерживает протоколы SSTP и IKEv2, а туннель устройства поддерживает IKEv2 только без поддержки отката SSTP.

Пользовательский туннель поддерживается на устройствах, присоединенных к домену, не присоединенных к домену (Рабочей группе) или в составе устройств, присоединенных к Azure AD, чтобы разрешить сценарии как для предприятия, так и для BYOD. Он доступен во всех выпусках Windows, а функции платформы доступны третьим сторонам посредством поддержки подключаемого модуля VPN UWP.

Туннель устройства можно настроить только на устройствах, присоединенных к домену, под управлением Windows 10 Корпоративная или для образовательных версий 1709 или более поздней версии. Сторонние средства управления туннелем устройства не поддерживаются. Туннель устройства не поддерживает использование таблицы политики разрешения имен (NRPT). Туннель устройства не поддерживает принудительный туннель. Его необходимо настроить как разделенный туннель.


## <a name="device-tunnel-requirements-and-features"></a>Требования и функции туннеля для устройства
Необходимо включить проверку подлинности сертификата компьютера для VPN-подключений и определить корневой центр сертификации для проверки подлинности входящих VPN-подключений.

```PowerShell
$VPNRootCertAuthority = "Common Name of trusted root certification authority"
$RootCACert = (Get-ChildItem -Path cert:LocalMachine\root | Where-Object {$_.Subject -Like "*$VPNRootCertAuthority*" })
Set-VpnAuthProtocol -UserAuthProtocolAccepted Certificate, EAP -RootCertificateNameToAccept $RootCACert -PassThru
```

![Функции и требования к туннелю устройств](../../media/device-tunnel-feature-and-requirements.png)

## <a name="vpn-device-tunnel-configuration"></a>Конфигурация туннеля VPN-устройства

Приведенный ниже пример XML-кода профиля предоставляет хорошее руководство для сценариев, в которых для туннеля устройства требуются только инициированные клиентом опросы.  Фильтры трафика используются, чтобы ограничить туннель устройства только трафиком управления.  Эта конфигурация хорошо подходит для Центр обновления Windows, типичных групповая политика (GP) и Microsoft Endpoint Configuration Manager обновления, а также VPN-подключения для первого входа без кэшированных учетных данных или сценариев сброса пароля.

Для инициированных сервером вариантов push-уведомлений, таких как служба удаленного управления Windows (WinRM), Remote GPUpdate и Remote Configuration Manager Update, необходимо разрешить входящий трафик в туннеле устройства, чтобы не использовать фильтры трафика.  Если в профиле туннеля устройства вы включите фильтры трафика, то туннель устройства отклоняет входящий трафик.  Это ограничение будет удалено в будущих выпусках.


### <a name="sample-vpn-profilexml"></a>Пример VPN-Профилексмл

Ниже приведен пример VPN-Профилексмл.

``` xml
<VPNProfile>
  <NativeProfile>
<Servers>vpn.contoso.com</Servers>
<NativeProtocolType>IKEv2</NativeProtocolType>
<Authentication>
  <MachineMethod>Certificate</MachineMethod>
</Authentication>
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>
 <!-- disable the addition of a class based route for the assigned IP address on the VPN interface -->
<DisableClassBasedDefaultRoute>true</DisableClassBasedDefaultRoute>
  </NativeProfile>
  <!-- use host routes(/32) to prevent routing conflicts -->
  <Route>
<Address>10.10.0.2</Address>
<PrefixSize>32</PrefixSize>
  </Route>
  <Route>
<Address>10.10.0.3</Address>
<PrefixSize>32</PrefixSize>
  </Route>
<!-- traffic filters for the routes specified above so that only this traffic can go over the device tunnel -->
  <TrafficFilter>
<RemoteAddressRanges>10.10.0.2, 10.10.0.3</RemoteAddressRanges>
  </TrafficFilter>
<!-- need to specify always on = true -->
  <AlwaysOn>true</AlwaysOn>
<!-- new node to specify that this is a device tunnel -->
 <DeviceTunnel>true</DeviceTunnel>
<!--new node to register client IP address in DNS to enable manage out -->
<RegisterDNS>true</RegisterDNS>
</VPNProfile>
```

В зависимости от потребностей каждого конкретного сценария развертывания другой компонент VPN, который можно настроить с помощью туннеля устройства, — это [Обнаружение доверенных сетей](/answers/topics/windows-server-infrastructure.html).

```
 <!-- inside/outside detection -->
  <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>
```

## <a name="deployment-and-testing"></a>Развертывание и тестирование

Туннели устройств можно настроить с помощью сценария Windows PowerShell и моста инструментарий управления Windows (WMI) (WMI). Туннель VPN-устройства Always On должен быть настроен в контексте **локальной системной** учетной записи. Для этого потребуется использовать [PsExec](/sysinternals/downloads/psexec), один из комплекта [PsTools](/sysinternals/downloads/pstools) , входящий в комплект служебных программ [Sysinternals](/sysinternals/) Suite.

Рекомендации по развертыванию для каждого устройства `(.\Device)` и профиля каждого пользователя `(.\User)` см. в статье [Использование сценариев PowerShell с поставщиком моста WMI](/windows/client-management/mdm/using-powershell-scripting-with-the-wmi-bridge-provider).

Выполните следующую команду Windows PowerShell, чтобы убедиться, что профиль устройства успешно развернут.

  ```powershell
  Get-VpnConnection -AllUserConnection
  ```

В выходных данных отображается список \- профилей VPN для всех устройств, развернутых на устройстве.

### <a name="example-windows-powershell-script"></a>Пример сценария Windows PowerShell

Для создания собственного скрипта для создания профиля можно использовать следующий сценарий Windows PowerShell.

```PowerShell
Param(
[string]$xmlFilePath,
[string]$ProfileName
)

$a = Test-Path $xmlFilePath
echo $a

$ProfileXML = Get-Content $xmlFilePath

echo $XML

$ProfileNameEscaped = $ProfileName -replace ' ', '%20'

$Version = 201606090004

$ProfileXML = $ProfileXML -replace '<', '&lt;'
$ProfileXML = $ProfileXML -replace '>', '&gt;'
$ProfileXML = $ProfileXML -replace '"', '&quot;'

$nodeCSPURI = './Vendor/MSFT/VPNv2'
$namespaceName = "root\cimv2\mdm\dmmap"
$className = "MDM_VPNv2_01"

$session = New-CimSession

try
{
$newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", 'String', 'Property')
$newInstance.CimInstanceProperties.Add($property)

$session.CreateInstance($namespaceName, $newInstance)
$Message = "Created $ProfileName profile."
Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to create $ProfileName profile: $_"
Write-Host "$Message"
exit
}
$Message = "Complete."
Write-Host "$Message"
```

## <a name="additional-resources"></a>Дополнительные ресурсы

Ниже приведены дополнительные ресурсы для помощи при развертывании VPN.

### <a name="vpn-client-configuration-resources"></a>Ресурсы конфигурации VPN-клиента

Ниже приведены ресурсы конфигурации VPN-клиента.

- [Создание профилей VPN в Configuration Manager](/configmgr/protect/deploy-use/create-vpn-profiles)
- [Настройка клиента Windows 10 Always On VPN-подключений](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [Параметры профиля VPN](/windows/access-protection/vpn/vpn-profile-options)

### <a name="remote-access-server-gateway-resources"></a>Ресурсы шлюза сервера удаленного доступа

Ниже приведены ресурсы шлюза сервера удаленного доступа (RAS).

- [Настройка RRAS с помощью сертификата проверки подлинности компьютера](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd458982(v=ws.11))
- [Устранение неполадок VPN-подключений по протоколу IKEv2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd941612(v=ws.10))
- [Настройка удаленного доступа на основе IKEv2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff687731(v=ws.10))

>[!IMPORTANT]
>При использовании туннеля устройства с шлюзом Microsoft RAS необходимо настроить сервер RRAS для поддержки проверки подлинности сертификата компьютера по протоколу IKEv2, включив параметр Разрешить проверку подлинности на основе **сертификата компьютера для** проверки подлинности IKEv2, как описано [здесь](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ee922682%28v=ws.10%29). После включения этого параметра настоятельно рекомендуется использовать командлет PowerShell **Set-впнауспротокол** вместе с необязательным параметром **рутцертификатенаметоакцепт** , чтобы убедиться, что подключения RRAS по протоколу IKEv2 разрешены только для сертификатов VPN-клиентов, которые связаны с явно определенным внутренним или частным корневым центром сертификации. Кроме того, необходимо внести изменения в хранилище **доверенных корневых центров сертификации** на сервере RRAS, чтобы убедиться, что он не содержит общедоступных центров сертификации, как описано [здесь](/archive/blogs/rrasblog/what-type-of-certificate-to-install-on-the-vpn-server). Аналогичные методы также могут быть рассмотрены для других VPN-шлюзов.