---
description: 'Дополнительные сведения: производительность шлюза Windows Server 2019'
title: Производительность шлюза Windows Server 2019
manager: grcusanz
ms.topic: how-to
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/22/2018
ms.openlocfilehash: 51cc64337029792fe8df724ad0d91515c3ab0eb8
ms.sourcegitcommit: fb2ae5e6040cbe6dde3a87aee4a78b08f9a9ea7c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2021
ms.locfileid: "98716450"
---
# <a name="windows-server-2019-gateway-performance"></a>Производительность шлюза Windows Server 2019

>Область применения: Windows Server 2019

В Windows Server 2016 одна из проблем клиента была невозможной для шлюза SDN в соответствии с требованиями к пропускной способности современных сетей. Пропускная способность сети туннелей IPsec и GRE была ограничена пропускной способностью одиночного подключения для подключения IPsec примерно 300 Мбит/с, а для подключения GRE — 2,5 Гбит/с.

Мы значительно улучшили Windows Server 2019, где числа соаринг до 1,8 Гбит/с и 15 Гбит/с для подключений IPsec и GRE соответственно. Все это, с значительным уменьшением количества циклов ЦП/за байт, обеспечивая высокую пропускную способность с высокой производительностью и меньшим потреблением ресурсов ЦП.

## <a name="enable-high-performance-with-gateways-in-windows-server-2019"></a>Обеспечение высокой производительности с помощью шлюзов в Windows Server 2019

Для **соединений GRE** после развертывания или обновления до Windows Server 2019, построенных на виртуальных машинах шлюза, следует автоматически увидеть улучшенную производительность. Ручные действия не участвуют.

Для **подключений IPsec** по умолчанию при создании подключения для виртуальных сетей вы получаете путь к данным и номера производительности Windows Server 2016. Чтобы включить путь к данным Windows Server 2019, выполните следующие действия.

   1. На виртуальной машине шлюза SDN перейдите в консоль **службы** (Services. msc).
   2. Найдите службу с именем **Служба шлюза Azure** и задайте для параметра Тип запуска значение **автоматически**.
   3. Перезапустите виртуальную машину шлюза.
      Активные подключения к этому шлюзу отработки отказа на виртуальную машину шлюза с избыточностью.
   4. Повторите предыдущие шаги для остальных виртуальных машин шлюза.

>[!TIP]
>Для достижения наилучшей производительности убедитесь, что параметры Цифертрансформатионконстант и Аусентикатионтрансформконстант в быстрого режима подключения IPsec используют набор шифров **GCMAES256** .
>
>Для максимальной производительности оборудование узла шлюза должно поддерживать наборы инструкций ЦП AES-NI и ПКЛМУЛКДК. Они доступны на любом Вестмере (32nm) и более поздней версии процессора Intel, за исключением моделей, где отключен AES-NI. Вы можете просмотреть документацию поставщика оборудования, чтобы узнать, поддерживает ли ЦП наборы инструкций ЦП AES-NI и ПКЛМУЛКДК.

Ниже приведен пример подключения IPsec с оптимальными алгоритмами безопасности.

```PowerShell
# NOTE: The virtual gateway must be created before creating the IPsec connection. More details here.
# Create a new object for Tenant Network IPsec Connection
$nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties

# Update the common object properties
$nwConnectionProperties.ConnectionType = "IPSec"
$nwConnectionProperties.OutboundKiloBitsPerSecond = 2000000
$nwConnectionProperties.InboundKiloBitsPerSecond = 2000000

# Update specific properties depending on the Connection Type
$nwConnectionProperties.IpSecConfiguration = New-Object Microsoft.Windows.NetworkController.IpSecConfiguration
$nwConnectionProperties.IpSecConfiguration.AuthenticationMethod = "PSK"
$nwConnectionProperties.IpSecConfiguration.SharedSecret = "111_aaa"

$nwConnectionProperties.IpSecConfiguration.QuickMode = New-Object Microsoft.Windows.NetworkController.QuickMode
$nwConnectionProperties.IpSecConfiguration.QuickMode.PerfectForwardSecrecy = "PFS2048"
$nwConnectionProperties.IpSecConfiguration.QuickMode.AuthenticationTransformationConstant = "GCMAES256"
$nwConnectionProperties.IpSecConfiguration.QuickMode.CipherTransformationConstant = "GCMAES256"
$nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeSeconds = 3600
$nwConnectionProperties.IpSecConfiguration.QuickMode.IdleDisconnectSeconds = 500
$nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeKiloBytes = 2000

$nwConnectionProperties.IpSecConfiguration.MainMode = New-Object Microsoft.Windows.NetworkController.MainMode
$nwConnectionProperties.IpSecConfiguration.MainMode.DiffieHellmanGroup = "Group2"
$nwConnectionProperties.IpSecConfiguration.MainMode.IntegrityAlgorithm = "SHA256"
$nwConnectionProperties.IpSecConfiguration.MainMode.EncryptionAlgorithm = "AES256"
$nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeSeconds = 28800
$nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeKiloBytes = 2000

# L3 specific configuration (leave blank for IPSec)
$nwConnectionProperties.IPAddresses = @()
$nwConnectionProperties.PeerIPAddresses = @()

# Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel
$nwConnectionProperties.Routes = @()
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo
$ipv4Route.DestinationPrefix = "<<On premise subnet that must be reachable over the VPN tunnel. Ex: 10.0.0.0/24>>"
$ipv4Route.metric = 10
$nwConnectionProperties.Routes += $ipv4Route

# Tunnel Destination (Remote Endpoint) Address
$nwConnectionProperties.DestinationIPAddress = "<<Public IP address of the On-Premise VPN gateway. Ex: 192.168.3.4>>"

# Add the new Network Connection for the tenant. Note that the virtual gateway must be created before creating the IPsec connection. $uri is the REST URI of your deployment and must be in the form of “https://<REST URI>”
New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_IPSecGW" -Properties $nwConnectionProperties -Force
```

## <a name="testing-results"></a>Результаты тестирования

Мы выполнили всестороннее тестирование производительности шлюзов SDN в наших тестовых лабораториях. В тестах мы сравнивали производительность сети шлюза с Windows Server 2019 в сценариях SDN и в сценариях, отличных от SDN. Результаты и сведения о настройке тестирования, полученные в блоге, можно найти [здесь](https://blogs.technet.microsoft.com/networking/2018/08/15/high-performance-gateways/).

---
