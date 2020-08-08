---
title: Кластеризация гостевых систем в виртуальной сети
description: Виртуальные машины, подключенные к виртуальной сети, могут использовать только IP-адреса, назначенные сетевому контроллеру для связи в сети.  Технологии кластеризации, для которых требуется плавающий IP-адрес, например отказоустойчивая кластеризация (Майкрософт), требуются дополнительные действия для правильной работы.
manager: grcusanz
ms.topic: article
ms.assetid: 8e9e5c81-aa61-479e-abaf-64c5e95f90dc
ms.author: grcusanz
author: AnirbanPaul
ms.date: 08/26/2018
ms.openlocfilehash: 6d597d4ced923c751e54ed4678ffb2d956a7b471
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87994772"
---
# <a name="guest-clustering-in-a-virtual-network"></a>Кластеризация гостевых систем в виртуальной сети

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Виртуальные машины, подключенные к виртуальной сети, могут использовать только IP-адреса, назначенные сетевому контроллеру для связи в сети.  Технологии кластеризации, для которых требуется плавающий IP-адрес, например отказоустойчивая кластеризация (Майкрософт), требуются дополнительные действия для правильной работы.

Для обеспечения доступности плавающего IP-адреса следует использовать программное обеспечение Load Balancer \( \) виртуального IP- \( адреса SLB \) .  Программная подсистема балансировки нагрузки должна быть настроена с проверкой работоспособности на порте этого IP-адреса, чтобы SLB направляли трафик на компьютер, на котором в данный момент находится этот IP-адрес.


## <a name="example-load-balancer-configuration"></a>Пример: Конфигурация подсистемы балансировки нагрузки

В этом примере предполагается, что вы уже создали виртуальные машины, которые станут узлами кластера, и подключили их к виртуальной сети.  Инструкции см. в статье [Создание виртуальной машины и подключение к виртуальной сети клиента или VLAN](./create-a-tenant-vm.md).

В этом примере вы создадите виртуальный IP-адрес (192.168.2.100) для представления плавающего IP-адреса кластера и настроите проверку работоспособности для мониторинга TCP-порта 59999, чтобы определить, какой узел является активным.

1. Выберите виртуальный IP-адрес.<p>Подготовьте, назначив IP-адрес виртуальной ЛС, который может быть любым неиспользуемым или зарезервированным адресом в той же подсети, что и узлы кластера.  VIP должен соответствовать плавающему адресу кластера.

   ```PowerShell
   $VIP = "192.168.2.100"
   $subnet = "Subnet2"
   $VirtualNetwork = "MyNetwork"
   $ResourceId = "MyNetwork_InternalVIP"
   ```

2. Создайте объект свойств балансировщика нагрузки.

   ```PowerShell
   $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

3. Создайте интерфейсный \- IP-адрес.

   ```PowerShell
   $LoadBalancerProperties.frontendipconfigurations += $FrontEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
   $FrontEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
   $FrontEnd.resourceId = "Frontend1"
   $FrontEnd.resourceRef = "/loadBalancers/$ResourceId/frontendIPConfigurations/$($FrontEnd.resourceId)"
   $FrontEnd.properties.subnet = new-object Microsoft.Windows.NetworkController.Subnet
   $FrontEnd.properties.subnet.ResourceRef = "/VirtualNetworks/MyNetwork/Subnets/Subnet2"
   $FrontEnd.properties.privateIPAddress = $VIP
   $FrontEnd.properties.privateIPAllocationMethod = "Static"
   ```

4. Создайте пул серверной части, \- который будет содержать узлы кластера.

   ```PowerShell
   $BackEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
   $BackEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties
   $BackEnd.resourceId = "Backend1"
   $BackEnd.resourceRef = "/loadBalancers/$ResourceId/backendAddressPools/$($BackEnd.resourceId)"
   $LoadBalancerProperties.backendAddressPools += $BackEnd
   ```

5. Добавьте пробу, чтобы определить, на каком узле кластера в данный момент активен плавающий адрес.

   >[!NOTE]
   >Пробный запрос к постоянному адресу виртуальной машины через порт, определенный ниже.  Порт должен отвечать только на активный узел.

   ```PowerShell
   $LoadBalancerProperties.probes += $lbprobe = new-object Microsoft.Windows.NetworkController.LoadBalancerProbe
   $lbprobe.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerProbeProperties

   $lbprobe.ResourceId = "Probe1"
   $lbprobe.resourceRef = "/loadBalancers/$ResourceId/Probes/$($lbprobe.resourceId)"
   $lbprobe.properties.protocol = "TCP"
   $lbprobe.properties.port = "59999"
   $lbprobe.properties.IntervalInSeconds = 5
   $lbprobe.properties.NumberOfProbes = 11
   ```

6. Добавьте правила балансировки нагрузки для TCP-порта 1433.<p>При необходимости можно изменить протокол и порт.  Кроме того, этот шаг можно повторить несколько раз для дополнительных портов и протколс на этом виртуальном IP-адресе.  Важно, чтобы для EnableFloatingIP было задано значение $true, так как это указывает подсистеме балансировки нагрузки отправить пакет на узел с исходным виртуальным IP-адресом.

   ```PowerShell
   $LoadBalancerProperties.loadbalancingRules += $lbrule = new-object Microsoft.Windows.NetworkController.LoadBalancingRule
   $lbrule.properties = new-object Microsoft.Windows.NetworkController.LoadBalancingRuleProperties
   $lbrule.ResourceId = "Rules1"

   $lbrule.properties.frontendipconfigurations += $FrontEnd
   $lbrule.properties.backendaddresspool = $BackEnd
   $lbrule.properties.protocol = "TCP"
   $lbrule.properties.frontendPort = $lbrule.properties.backendPort = 1433
   $lbrule.properties.IdleTimeoutInMinutes = 4
   $lbrule.properties.EnableFloatingIP = $true
   $lbrule.properties.Probe = $lbprobe
   ```

7. Создайте подсистему балансировки нагрузки в сетевом контроллере.

   ```PowerShell
   $lb = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $ResourceId -Properties $LoadBalancerProperties -Force
   ```

8. Добавьте узлы кластера в серверный пул.<p>В пул можно добавить столько узлов, сколько требуется для кластера.

   ```PowerShell
   # Cluster Node 1

   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode1_Network-Adapter"
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force

    # Cluster Node 2

   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode2_Network-Adapter"
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force
   ```

   После создания подсистемы балансировки нагрузки и добавления сетевых интерфейсов в серверный пул можно приступать к настройке кластера.

9. Используемых Если вы используете отказоустойчивый кластер Майкрософт, перейдите к следующему примеру.

## <a name="example-2-configuring-a-microsoft-failover-cluster"></a>Пример 2. Настройка отказоустойчивого кластера Microsoft

Для настройки отказоустойчивого кластера можно выполнить следующие действия.

1. Установка и Настройка свойств для отказоустойчивого кластера.

   ```PowerShell
   add-windowsfeature failover-clustering -IncludeManagementTools
   Import-module failoverclusters

   $ClusterName = "MyCluster"

   $ClusterNetworkName = "Cluster Network 1"
   $IPResourceName =
   $ILBIP = "192.168.2.100"

   $nodes = @("DB1", "DB2")
   ```

2. Создайте кластер на одном узле.

   ```PowerShell
   New-Cluster -Name $ClusterName -NoStorage -Node $nodes[0]
   ```

3. Останавливает ресурс кластера.

   ```PowerShell
   Stop-ClusterResource "Cluster Name" 
   ```

4. Задайте IP-адрес кластера и порт пробы.<p>IP-адрес должен соответствовать интерфейсному IP-адресу, используемому в предыдущем примере, а порт пробы должен соответствовать порту пробы в предыдущем примере.

   ```PowerShell
   Get-ClusterResource "Cluster IP Address" | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

5. Запустите ресурсы кластера.

   ```PowerShell
    Start-ClusterResource "Cluster IP Address"  -Wait 60 
    Start-ClusterResource "Cluster Name"  -Wait 60 
   ```

6. Добавьте остальные узлы.

   ```PowerShell
   Add-ClusterNode $nodes[1]
   ```

_**Кластер активен.**_ Трафик, поступающий в виртуальный IP-адрес указанного порта, направляется на активный узел.

---