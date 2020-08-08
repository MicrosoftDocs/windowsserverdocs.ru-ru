---
title: Настройка программного балансировщика нагрузки для балансировки нагрузки и преобразования сетевых адресов (NAT)
description: Эта статья является частью программно-определяемого сетевого руководства по управлению рабочими нагрузками клиентов и виртуальными сетями в Windows Server 2016.
manager: grcusanz
ms.topic: article
ms.assetid: 73bff8ba-939d-40d8-b1e5-3ba3ed5439c3
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/23/2018
ms.openlocfilehash: e7488c546753594f61e034b271fcaddfd52a0233
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954050"
---
# <a name="configure-the-software-load-balancer-for-load-balancing-and-network-address-translation-nat"></a>Настройка программного балансировщика нагрузки для балансировки нагрузки и преобразования сетевых адресов (NAT)

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

С помощью этого раздела вы узнаете, как использовать программно определяемую сетевую \( \) подсистему балансировки нагрузки Sdn \( \) для обеспечения исходящего трафика преобразования сетевых адресов \( NAT \) , входящего трафика NAT или балансировки нагрузки между несколькими экземплярами приложения.

## <a name="software-load-balancer-overview"></a>Обзор программного Load Balancer

Программное обеспечение SDN Load Balancer \( SLB \) обеспечивает высокую доступность и производительность сети для приложений. Это \( TCP-балансировщик нагрузки уровня 4, \) который распределяет входящий трафик между работоспособными экземплярами службы в облачных службах или виртуальных машинах, определенных в наборе подсистемы балансировки нагрузки.

Настройте SLB, чтобы сделать следующее:

- Балансировка нагрузки входящего трафика, внешнего в виртуальной сети, на виртуальные машины виртуальных машин \( \) , также называемая балансировкой нагрузки общедоступных виртуальных IP-адресов.
- Балансировка нагрузки входящего трафика между виртуальными машинами в виртуальной сети, между виртуальными машинами в облачных службах или между локальными компьютерами и виртуальными машинами в распределенной виртуальной сети.
- Пересылка сетевого трафика виртуальной машины из виртуальной сети во внешние назначения с помощью преобразования сетевых адресов (NAT), также называемого исходящим NAT.
- Перенаправлять внешний трафик на определенную виртуальную машину, также называемую входящим NAT.




## <a name="example-create-a-public-vip-for-load-balancing-a-pool-of-two-vms-on-a-virtual-network"></a>Пример. Создание общедоступного виртуального IP-адреса для балансировки нагрузки пула из двух виртуальных машин в виртуальной сети

В этом примере вы создадите объект балансировщика нагрузки с общедоступным виртуальным IP-адресом и двумя виртуальными машинами в качестве членов пула для обслуживания запросов к виртуальному IP-адресу. В этом примере кода также добавляется проба работоспособности HTTP для определения того, что один из членов пула не отвечает.

1. Подготовьте объект балансировщика нагрузки.

   ```PowerShell
    import-module NetworkController

    $URI = "https://sdn.contoso.com"

    $LBResourceId = "LB2"

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

2. Назначьте IP-адрес внешнего интерфейса, который обычно называется виртуальным IP (VIP).<p>Виртуальный IP-адрес должен быть неиспользуемым в одном из пулов IP-адресов логической сети, предоставленных диспетчеру подсистемы балансировки нагрузки.

   ```PowerShell
    $VIPIP = "10.127.134.5"
    $VIPLogicalNetwork = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "PublicVIP" -PassInnerException

    $FrontEndIPConfig = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
    $FrontEndIPConfig.ResourceId = "FE1"
    $FrontEndIPConfig.ResourceRef = "/loadBalancers/$LBResourceId/frontendIPConfigurations/$($FrontEndIPConfig.ResourceId)"

    $FrontEndIPConfig.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
    $FrontEndIPConfig.Properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $FrontEndIPConfig.Properties.Subnet.ResourceRef = $VIPLogicalNetwork.Properties.Subnets[0].ResourceRef
    $FrontEndIPConfig.Properties.PrivateIPAddress = $VIPIP
    $FrontEndIPConfig.Properties.PrivateIPAllocationMethod = "Static"

    $LoadBalancerProperties.FrontEndIPConfigurations += $FrontEndIPConfig
   ```

3. Выделите пул внутренних адресов, содержащий динамические IP-адреса (DIP), которые составляют элементы набора виртуальных машин с балансировкой нагрузки.

   ```PowerShell
    $BackEndAddressPool = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEndAddressPool.ResourceId = "BE1"
    $BackEndAddressPool.ResourceRef = "/loadBalancers/$LBResourceId/backendAddressPools/$($BackEndAddressPool.ResourceId)"

    $BackEndAddressPool.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties

    $LoadBalancerProperties.backendAddressPools += $BackEndAddressPool
   ```

4. Определите проверку работоспособности, используемую подсистемой балансировки нагрузки для определения состояния работоспособности членов внутреннего пула.<p>В этом примере определяется HTTP-зонд, который запрашивает RequestPath "/health.htm".  Запрос выполняется каждые 5 секунд, как указано свойством IntervalInSeconds.<p>Зонд работоспособности должен получить код HTTP-ответа 200 для 11 последовательных запросов, чтобы проверить, что серверный IP-адрес должен быть работоспособным. Если серверный IP-адрес находится в неработоспособном состоянии, он не получает трафик от балансировщика нагрузки.

   >[!IMPORTANT]
   >Не блокируйте трафик с первого IP-адреса в подсети или из него для любых списков управления доступом (ACL), применяемых к внутреннему IP-адресу, так как это точка происхождения для проб.

   Используйте следующий пример для определения пробы работоспособности.

   ```PowerShell
    $Probe = new-object Microsoft.Windows.NetworkController.LoadBalancerProbe
    $Probe.ResourceId = "Probe1"
    $Probe.ResourceRef = "/loadBalancers/$LBResourceId/Probes/$($Probe.ResourceId)"

    $Probe.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerProbeProperties
    $Probe.properties.Protocol = "HTTP"
    $Probe.properties.Port = "80"
    $Probe.properties.RequestPath = "/health.htm"
    $Probe.properties.IntervalInSeconds = 5
    $Probe.properties.NumberOfProbes = 11

    $LoadBalancerProperties.Probes += $Probe
   ```

5. Определите правило балансировки нагрузки для отправки трафика, поступающих на клиентский IP-адрес, на серверный IP.  В этом примере серверный пул получает трафик TCP на порт 80.<p>Для определения правила балансировки нагрузки используйте следующий пример:

   ```PowerShell
   $Rule = new-object Microsoft.Windows.NetworkController.LoadBalancingRule
   $Rule.ResourceId = "webserver1"

   $Rule.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancingRuleProperties
   $Rule.Properties.FrontEndIPConfigurations += $FrontEndIPConfig
   $Rule.Properties.backendaddresspool = $BackEndAddressPool
   $Rule.Properties.protocol = "TCP"
   $Rule.Properties.FrontEndPort = 80
   $Rule.Properties.BackEndPort = 80
   $Rule.Properties.IdleTimeoutInMinutes = 4
   $Rule.Properties.Probe = $Probe

   $LoadBalancerProperties.loadbalancingRules += $Rule
   ```

6. Добавьте конфигурацию подсистемы балансировки нагрузки в сетевой контроллер.<p>Используйте следующий пример, чтобы добавить конфигурацию подсистемы балансировки нагрузки в сетевой контроллер:

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

7. Выполните следующий пример, чтобы добавить сетевые интерфейсы в этот пул серверной части.


## <a name="example-use-slb-for-outbound-nat"></a>Пример. Использование SLB для исходящего NAT

В этом примере вы настраиваете SLB с внутренним пулом, обеспечивающим возможность исходящего трафика NAT для виртуальной машины в частном адресном пространстве виртуальной сети, чтобы обеспечить доступ к исходящим подключениям через Интернет.

1. Создайте свойства балансировщика нагрузки, IP-адрес внешнего интерфейса и пул внутренних серверов.

   ```PowerShell
    import-module NetworkController
    $URI = "https://sdn.contoso.com"

    $LBResourceId = "OutboundNATMMembers"
    $VIPIP = "10.127.134.6"

    $VIPLogicalNetwork = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "PublicVIP" -PassInnerException

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties

    $FrontEndIPConfig = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
    $FrontEndIPConfig.ResourceId = "FE1"
    $FrontEndIPConfig.ResourceRef = "/loadBalancers/$LBResourceId/frontendIPConfigurations/$($FrontEndIPConfig.ResourceId)"

    $FrontEndIPConfig.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
    $FrontEndIPConfig.Properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $FrontEndIPConfig.Properties.Subnet.ResourceRef = $VIPLogicalNetwork.Properties.Subnets[0].ResourceRef
    $FrontEndIPConfig.Properties.PrivateIPAddress = $VIPIP
    $FrontEndIPConfig.Properties.PrivateIPAllocationMethod = "Static"

    $LoadBalancerProperties.FrontEndIPConfigurations += $FrontEndIPConfig

    $BackEndAddressPool = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEndAddressPool.ResourceId = "BE1"
    $BackEndAddressPool.ResourceRef = "/loadBalancers/$LBResourceId/backendAddressPools/$($BackEndAddressPool.ResourceId)"
    $BackEndAddressPool.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties

    $LoadBalancerProperties.backendAddressPools += $BackEndAddressPool
   ```

2. Определите правило NAT для исходящего трафика.

   ```PowerShell
    $OutboundNAT = new-object Microsoft.Windows.NetworkController.LoadBalancerOutboundNatRule
    $OutboundNAT.ResourceId = "onat1"

    $OutboundNAT.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerOutboundNatRuleProperties
    $OutboundNAT.properties.frontendipconfigurations += $FrontEndIPConfig
    $OutboundNAT.properties.backendaddresspool = $BackEndAddressPool
    $OutboundNAT.properties.protocol = "ALL"

    $LoadBalancerProperties.OutboundNatRules += $OutboundNAT
   ```

3. Добавьте объект балансировщика нагрузки в сетевом контроллере.

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

4. Выполните следующий пример, чтобы добавить сетевые интерфейсы, к которым требуется предоставить доступ в Интернет.

## <a name="example-add-network-interfaces-to-the-back-end-pool"></a>Пример. Добавление сетевых интерфейсов в серверный пул
В этом примере вы добавляете сетевые интерфейсы в пул серверной части.  Этот шаг необходимо повторить для каждого сетевого интерфейса, который может обрабатывать запросы к виртуальному IP-адресу.

Кроме того, этот процесс можно повторить на одном сетевом интерфейсе, чтобы добавить его в несколько объектов подсистемы балансировки нагрузки. Например, если у вас есть объект подсистемы балансировки нагрузки для виртуального IP-адреса сервера и отдельный объект балансировщика нагрузки для обеспечения исходящего трафика NAT.

1. Получите объект балансировщика нагрузки, содержащий серверный пул, для добавления сетевого интерфейса.

   ```PowerShell
   $lbresourceid = "LB2"
   $lb = get-networkcontrollerloadbalancer -connectionuri $uri -resourceID $LBResourceId -PassInnerException
   ```

2. Получите сетевой интерфейс и добавьте пул баккендаддресс в массив loadbalancerbackendaddresspools.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -PassInnerException
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   ```

3. Установите сетевой интерфейс, чтобы применить изменение.

   ```PowerShell
   new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -properties $nic.properties -force -PassInnerException
   ```


## <a name="example-use-the-software-load-balancer-for-forwarding-traffic"></a>Пример. Использование Load Balancer программного обеспечения для перенаправления трафика
Если необходимо подключить виртуальный IP-адрес к одному сетевому интерфейсу в виртуальной сети без определения отдельных портов, можно создать правило пересылки L3.  Это правило перенаправляет весь входящий и исходящий трафик виртуальной машины с помощью назначенного виртуального IP-адреса, содержащегося в объекте PublicIPAddress.

Если виртуальный IP-адрес и DIP определены как одна и та же подсеть, это эквивалентно выполнению пересылки L3 без преобразования сетевых адресов (NAT).

>[!NOTE]
>Для этого процесса не требуется создавать объект балансировщика нагрузки.  Назначение PublicIPAddress для сетевого интерфейса достаточно для того, чтобы Load Balancer программного обеспечения выполняла конфигурацию.


1. Создайте объект общедоступного IP-адреса, который будет содержать VIP.

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.ipaddress = "10.127.134.7"
   $publicIPProperties.PublicIPAllocationMethod = "static"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. Назначьте PublicIPAddress сетевому интерфейсу.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```

## <a name="example-use-the-software-load-balancer-for-forwarding-traffic-with-a-dynamically-allocated-vip"></a>Пример. Использование Load Balancer программного обеспечения для перенаправления трафика с динамически выделенным виртуальным IP-адресом
В этом примере повторяется то же действие, что и в предыдущем примере, но он автоматически выделяет VIP из доступного пула виртуальных IP-адресов в подсистеме балансировки нагрузки вместо указания конкретного IP-адреса.

1. Создайте объект общедоступного IP-адреса, который будет содержать VIP.

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.PublicIPAllocationMethod = "dynamic"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. Запросите ресурс PublicIPAddress, чтобы определить, какой IP-адрес был назначен.

   ```PowerShell
    (Get-NetworkControllerPublicIpAddress -ConnectionUri $uri -ResourceId "MyPIP").properties
   ```

   Свойство IpAddress содержит назначенный адрес.  Выходные данные будут выглядеть следующим образом.
   ```
    Counters                 : {}
    ConfigurationState       :
    IpAddress                : 10.127.134.2
    PublicIPAddressVersion   : IPv4
    PublicIPAllocationMethod : Dynamic
    IdleTimeoutInMinutes     : 4
    DnsSettings              :
    ProvisioningState        : Succeeded
    IpConfiguration          :
    PreviousIpConfiguration  :
   ```

3. Назначьте PublicIPAddress сетевому интерфейсу.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```
   ## <a name="example-remove-a-publicip-address-that-is-being-used-for-forwarding-traffic-and-return-it-to-the-vip-pool"></a>Пример. Удаление адреса PublicIP, который используется для перенаправления трафика, и его возврата в пул виртуальных IP-адресов
   В этом примере удаляется ресурс PublicIPAddress, созданный в предыдущих примерах.  После удаления PublicIPAddress ссылка на PublicIPAddress будет автоматически удалена из сетевого интерфейса, пересылка трафика будет перенаправлена, а IP-адрес будет возвращен в пул общедоступных VIP для повторного использования.

4. Удаление PublicIP

   ```PowerShell
   Remove-NetworkControllerPublicIPAddress -ConnectionURI $uri -ResourceId "MyPIP"
   ```

---


