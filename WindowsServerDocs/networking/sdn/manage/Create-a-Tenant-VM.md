---
title: Создание виртуальной машины и подключение к виртуальной сети или виртуальной локальной сети клиента
description: В этом разделе мы покажем, как создать виртуальную машину клиента и подключить ее к виртуальной сети, созданной с помощью виртуализации сети Hyper-V или виртуальной локальной сети (VLAN).
manager: grcusanz
ms.topic: article
ms.assetid: 3c62f533-1815-4f08-96b1-dc271f5a2b36
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/24/2018
ms.openlocfilehash: 2ca1c308ee38726d02ef19ebdfa4c83086fef0a7
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995152"
---
# <a name="create-a-vm-and-connect-to-a-tenant-virtual-network-or-vlan"></a>Создание виртуальной машины и подключение к виртуальной сети или виртуальной локальной сети клиента

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе вы создадите виртуальную машину клиента и подключите ее к виртуальной сети, созданной с помощью виртуализации сети Hyper-V или виртуальной локальной сети (VLAN). Командлеты сетевого контроллера Windows PowerShell можно использовать для подключения к виртуальной сети или Нетворкконтроллеррестврапперс для подключения к виртуальной ЛС.

Используйте описанные в этом разделе процессы для развертывания виртуальных устройств. С помощью нескольких дополнительных действий можно настроить устройства для обработки или проверки пакетов данных, которые передаются на другие виртуальные машины в виртуальной сети или с других виртуальных машин.

В подразделах этого раздела приведены примеры команд Windows PowerShell, которые содержат примеры значений для многих параметров. Перед выполнением этих команд обязательно замените примеры значений в этих командах значениями, подходящими для вашего развертывания.


## <a name="prerequisites"></a>Предварительные требования

1. Сетевые адаптеры виртуальной машины, созданные со статическими MAC-адресами в течение времени существования виртуальной машины.<p>Если MAC-адрес изменяется во время существования виртуальной машины, сетевой контроллер не может настроить необходимую политику для этого сетевого адаптера. Если не настроить политику для сети, сетевой адаптер не сможет обработать сетевой трафик и связь с сетью завершится сбоем.

2. Если виртуальной машине требуется доступ к сети при запуске, не запускайте виртуальную машину до установки идентификатора интерфейса для порта сетевого адаптера виртуальной машины. Если вы запускаете виртуальную машину перед заданием идентификатора интерфейса, а сетевой интерфейс не существует, виртуальная машина не сможет связаться с сетью в сетевом контроллере и применить все политики.

3. Если вам нужны настраиваемые списки ACL для этого сетевого интерфейса, создайте список ACL, следуя инструкциям в разделе [Использование списков управления доступом (ACL) для управления потоком сетевого трафика центра обработки данных](./use-acls-for-traffic-flow.md) .

Прежде чем использовать этот пример команды, убедитесь, что вы уже создали виртуальную сеть. Дополнительные сведения см. в [статье Создание, удаление или обновление виртуальных сетей клиента](./create,-delete,-or-update-tenant-virtual-networks.md).

## <a name="create-a-vm-and-connect-to-a-virtual-network-by-using-the-windows-powershell-network-controller-cmdlets"></a>Создание виртуальной машины и подключение к виртуальной сети с помощью командлетов сетевого контроллера Windows PowerShell


1. Создайте виртуальную машину с сетевым адаптером виртуальной машины со статическим MAC-адресом.

   ```PowerShell
   New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch"

   Set-VM -Name "MyVM" -ProcessorCount 4

   Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55"
   ```

2. Получите виртуальную сеть, содержащую подсеть, к которой необходимо подключить сетевой адаптер.

   ```Powershell
   $vnet = get-networkcontrollervirtualnetwork -connectionuri $uri -ResourceId "Contoso_WebTier"
   ```

3. Создайте объект сетевого интерфейса в сетевом контроллере.

   >[!TIP]
   >На этом шаге вы используете пользовательский ACL.

   ```PowerShell
   $vmnicproperties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceProperties
   $vmnicproperties.PrivateMacAddress = "001122334455"
   $vmnicproperties.PrivateMacAllocationMethod = "Static"
   $vmnicproperties.IsPrimary = $true

   $vmnicproperties.DnsSettings = new-object Microsoft.Windows.NetworkController.NetworkInterfaceDnsSettings
   $vmnicproperties.DnsSettings.DnsServers = @("24.30.1.11", "24.30.1.12")

   $ipconfiguration = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
   $ipconfiguration.resourceid = "MyVM_IP1"
   $ipconfiguration.properties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties
   $ipconfiguration.properties.PrivateIPAddress = "24.30.1.101"
   $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"

   $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
   $ipconfiguration.properties.subnet.ResourceRef = $vnet.Properties.Subnets[0].ResourceRef

   $vmnicproperties.IpConfigurations = @($ipconfiguration)
   New-NetworkControllerNetworkInterface –ResourceID "MyVM_Ethernet1" –Properties $vmnicproperties –ConnectionUri $uri
   ```

4. Получите InstanceId для сетевого интерфейса от сетевого контроллера.

   ```PowerShell
    $nic = Get-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId "MyVM-Ethernet1"
   ```

5. Задайте идентификатор интерфейса для порта сетевого адаптера виртуальной машины Hyper-V.

   >[!NOTE]
   >Эти команды необходимо выполнить на узле Hyper-V, на котором установлена виртуальная машина.

   ```PowerShell
   #Do not change the hardcoded IDs in this section, because they are fixed values and must not change.

   $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"

   $vmNics = Get-VMNetworkAdapter -VMName "MyVM"

   $CurrentFeature = Get-VMSwitchExtensionPortFeature -FeatureId $FeatureId -VMNetworkAdapter $vmNics

   if ($CurrentFeature -eq $null)
   {
   $Feature = Get-VMSystemSwitchExtensionPortFeature -FeatureId $FeatureId

   $Feature.SettingData.ProfileId = "{$($nic.InstanceId)}"
   $Feature.SettingData.NetCfgInstanceId = "{56785678-a0e5-4a26-bc9b-c0cba27311a3}"
   $Feature.SettingData.CdnLabelString = "TestCdn"
   $Feature.SettingData.CdnLabelId = 1111
   $Feature.SettingData.ProfileName = "Testprofile"
   $Feature.SettingData.VendorId = "{1FA41B39-B444-4E43-B35A-E1F7985FD548}"
   $Feature.SettingData.VendorName = "NetworkController"
   $Feature.SettingData.ProfileData = 1

   Add-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature  $Feature -VMNetworkAdapter $vmNics
   }
   else
   {
   $CurrentFeature.SettingData.ProfileId = "{$($nic.InstanceId)}"
   $CurrentFeature.SettingData.ProfileData = 1

   Set-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature $CurrentFeature  -VMNetworkAdapter $vmNic
   }
   ```

6. Запустите виртуальную машину.

   ```PowerShell
    Get-VM -Name "MyVM" | Start-VM
   ```

Вы успешно создали виртуальную машину, подключили ее к виртуальной сети клиента и запустили виртуальную машину, чтобы она могла обрабатывать рабочие нагрузки клиента.

## <a name="create-a-vm-and-connect-to-a-vlan-by-using-networkcontrollerrestwrappers"></a>Создание виртуальной машины и подключение к виртуальной ЛС с помощью Нетворкконтроллеррестврапперс


1. Создайте виртуальную машину и назначьте виртуальной машине статический MAC-адрес.

   ```PowerShell
   New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch"

   Set-VM -Name "MyVM" -ProcessorCount 4

   Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55"
   ```

2. Задайте идентификатор виртуальной ЛС для сетевого адаптера виртуальной машины.

   ```PowerShell
   Set-VMNetworkAdapterIsolation –VMName "MyVM" -AllowUntaggedTraffic $true -IsolationMode VLAN -DefaultIsolationId 123
   ```

3. Получите подсеть логической сети и создайте сетевой интерфейс.

   ```PowerShell
    $logicalnet = get-networkcontrollerLogicalNetwork -connectionuri $uri -ResourceId "00000000-2222-1111-9999-000000000002"

    $vmnicproperties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceProperties
    $vmnicproperties.PrivateMacAddress = "00-1D-C8-B7-01-02"
    $vmnicproperties.PrivateMacAllocationMethod = "Static"
    $vmnicproperties.IsPrimary = $true

    $vmnicproperties.DnsSettings = new-object Microsoft.Windows.NetworkController.NetworkInterfaceDnsSettings
    $vmnicproperties.DnsSettings.DnsServers = $logicalnet.Properties.Subnets[0].DNSServers

    $ipconfiguration = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
    $ipconfiguration.resourceid = "MyVM_Ip1"
    $ipconfiguration.properties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties
    $ipconfiguration.properties.PrivateIPAddress = "10.127.132.177"
    $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"

    $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $ipconfiguration.properties.subnet.ResourceRef = $logicalnet.Properties.Subnets[0].ResourceRef

    $vmnicproperties.IpConfigurations = @($ipconfiguration)
    $vnic = New-NetworkControllerNetworkInterface –ResourceID "MyVM_Ethernet1" –Properties $vmnicproperties –ConnectionUri $uri

    $vnic.InstanceId
   ```

4. Задайте InstanceId на порте Hyper-V.

   ```PowerShell
   #The hardcoded Ids in this section are fixed values and must not change.
   $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"

   $vmNics = Get-VMNetworkAdapter -VMName "MyVM"

   $CurrentFeature = Get-VMSwitchExtensionPortFeature -FeatureId $FeatureId -VMNetworkAdapter $vmNic

   if ($CurrentFeature -eq $null)
   {
       $Feature = Get-VMSystemSwitchExtensionFeature -FeatureId $FeatureId

       $Feature.SettingData.ProfileId = "{$InstanceId}"
       $Feature.SettingData.NetCfgInstanceId = "{56785678-a0e5-4a26-bc9b-c0cba27311a3}"
       $Feature.SettingData.CdnLabelString = "TestCdn"
       $Feature.SettingData.CdnLabelId = 1111
       $Feature.SettingData.ProfileName = "Testprofile"
       $Feature.SettingData.VendorId = "{1FA41B39-B444-4E43-B35A-E1F7985FD548}"
       $Feature.SettingData.VendorName = "NetworkController"
       $Feature.SettingData.ProfileData = 1

       Add-VMSwitchExtensionFeature -VMSwitchExtensionFeature  $Feature -VMNetworkAdapter $vmNic
   }
   else
   {
       $CurrentFeature.SettingData.ProfileId = "{$InstanceId}"
       $CurrentFeature.SettingData.ProfileData = 1

       Set-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature $CurrentFeature  -VMNetworkAdapter $vmNic
   }
   ```

5. Запустите виртуальную машину.

   ```PowerShell
   Get-VM -Name "MyVM" | Start-VM
   ```

Вы успешно создали виртуальную машину, подключили ее к виртуальной ЛС и запустили ВИРТУАЛЬную машину, чтобы она могла обрабатывать рабочие нагрузки клиента.