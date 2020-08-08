---
title: Межрегиональная межкластерная репликация хранилища в Azure
description: Репликация между кластером и хранилищем кластера в Azure
author: arduppal
ms.author: arduppal
ms.date: 12/19/2018
ms.topic: article
manager: mchad
ms.openlocfilehash: cb1b712e62b3b77def304526c7b65fd5187b56d5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939363"
---
# <a name="cluster-to-cluster-storage-replica-cross-region-in-azure"></a>Межрегиональная межкластерная репликация хранилища в Azure

> Применяется к: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)

Вы можете настроить кластеры на реплики хранилища кластера для приложений в разных регионах в Azure. В приведенных ниже примерах мы используем кластер из двух узлов, но Реплика хранилища кластера не ограничена кластером из двух узлов. На рисунке ниже показан распределенный кластер с двумя узлами, который может взаимодействовать друг с другом, находится в одном домене и находится в разных регионах.

Просмотрите видеоролик ниже, чтобы получить полный пошаговый обзор процесса.
> [!video https://www.microsoft.com/videoplayer/embed/RE26xeW]

![Схема архитектуры, демонстрирующий SR C2C в Azure в одном регионе.](media/Cluster-to-cluster-azure-cross-region/architecture.png)
> [!IMPORTANT]
> Все примеры, на которые указывают ссылки, относятся к иллюстрации выше.


1. В портал Azure создайте [группы ресурсов](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup) в двух разных регионах.

    Например, **SR-AZ2AZ** в **Западная часть США 2** и **SR-АЗКРОСС** в **западной центральной части США**, как показано выше.

2. Создайте две группы [доступности](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM), по одной в каждой группе ресурсов для каждого кластера.
    - Группа доступности (**az2azAS1**) в (**SR-AZ2AZ**)
    - Группа доступности (**азкросс-AS**) в (**SR-азкросс**)

3. создание двух виртуальных сетей;
   - Создайте [виртуальную сеть](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**az2az-vnet**) в первой группе ресурсов (**SR-az2az**) с одной подсетью и одной подсетью шлюза.
   - Создайте [виртуальную сеть](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**азкросс-vnet**) во второй группе ресурсов (**SR-азкросс**) с одной подсетью и одной подсетью шлюза.

4. Создание двух групп безопасности сети
   - Создайте [группу безопасности сети](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**az2az-NSG**) в первой группе ресурсов (**SR-az2az**).
   - Создайте [группу безопасности сети](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**азкросс-NSG**) во второй группе ресурсов (**SR-азкросс**).

   Добавьте одно правило безопасности входящего трафика для RDP: 3389 в обе группы безопасности сети. Вы можете удалить это правило после завершения установки.

5. Создайте [виртуальные машины](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM) Windows Server в ранее созданных группах ресурсов.

   Контроллер домена (**az2azDC**). Вы можете создать третью группу доступности для контроллера домена или добавить контроллер домена в одну из двух групп доступности. Если вы добавляете это в группу доступности, созданную для двух кластеров, назначьте ей Стандартный общедоступный IP-адрес во время создания виртуальной машины.
      - Установите службу домен Active Directory.
      - Создание домена (contoso.com)
      - Создание пользователя с правами администратора (contosoadmin)

   Создайте две виртуальные машины (**az2az1**, **az2az2**) в группе ресурсов (**SR-AZ2AZ**) с помощью виртуальной сети (**AZ2AZ-vnet**) и группы безопасности сети (**AZ2AZ-NSG**) в группе доступности (**az2azAS1**). Назначьте стандартные общедоступные IP-адреса каждой виртуальной машине во время создания.
      - Добавьте по меньшей мере два управляемых диска на каждый компьютер.
      - Установка отказоустойчивой кластеризации и функции реплики хранилища

   Создайте две виртуальные машины (**azcross1**, **azcross2**) в группе ресурсов (**SR-азкросс**) с помощью виртуальной сети (**азкросс-vnet**) и группы безопасности сети (**азкросс-NSG**) в группе доступности (**азкросс-AS**). Назначение стандартных общедоступных IP-адресов каждой виртуальной машине во время создания
      - Добавьте по меньшей мере два управляемых диска на каждый компьютер.
      - Установка отказоустойчивой кластеризации и функции реплики хранилища

   Подключите все узлы к домену и предоставьте права администратора для ранее созданного пользователя.

   Измените DNS-сервер виртуальной сети на частный IP-адрес контроллера домена.
   - В этом примере контроллер домена **az2azDC** имеет частный IP-адрес (10.3.0.8). В виртуальной сети (**az2az-vnet** и **азкросс-vnet**) измените DNS-сервер 10.3.0.8.

     В этом примере Подключите все узлы к "contoso.com" и предоставьте права администратора для "contosoadmin".
   - Войдите как contosoadmin со всех узлов.

6. Создайте кластеры (**SRAZC1**, **сразкросс**).

   Ниже приведены команды PowerShell для примера.
   ```powershell
      New-Cluster -Name SRAZC1 -Node az2az1,az2az2 –StaticAddress 10.3.0.100
   ```
   ```powershell
      New-Cluster -Name SRAZCross -Node azcross1,azcross2 –StaticAddress 10.0.0.10
   ```

7. Включите Локальные дисковые пространства.

   ```powershell
      Enable-clusterS2D
   ```

   > [!NOTE]
   > Для каждого кластера создайте виртуальный диск и том. Один для данных, а другой для журнала.

8. Создайте внутренний [Load Balancer](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM) SKU "Стандартный" для каждого кластера (**azlbr1**, **азлбазкросс**).

   Укажите IP-адрес кластера в виде статического частного IP-адреса для балансировщика нагрузки.
      - azlbr1 => интерфейсный IP-адрес: 10.3.0.100 (выбор неиспользуемого IP-адреса из подсети виртуальной сети (**az2az-vnet**))
      - Создайте серверный пул для каждой подсистемы балансировки нагрузки. Добавьте связанные узлы кластера.
      - Создание проверки работоспособности: порт 59999
      - Создать правило балансировки нагрузки: разрешить порты с высоким уровнем доступности с включенным плавающим IP-адресом.

   Укажите IP-адрес кластера в виде статического частного IP-адреса для балансировщика нагрузки.
      - азлбазкросс => интерфейсный IP-адрес: 10.0.0.10 (выбор неиспользуемого IP-адреса из подсети виртуальной сети (**азкросс-vnet**))
      - Создайте серверный пул для каждой подсистемы балансировки нагрузки. Добавьте связанные узлы кластера.
      - Создание проверки работоспособности: порт 59999
      - Создать правило балансировки нагрузки: разрешить порты с высоким уровнем доступности с включенным плавающим IP-адресом.

9. Создайте [шлюз виртуальной сети](https://ms.portal.azure.com/#create/Microsoft.VirtualNetworkGateway-ARM) для подключения между виртуальными сетями.

   - Создание первого шлюза виртуальной сети (**az2az-внетгатевай**) в первой группе ресурсов (**SR-az2az**)
   - Тип шлюза — VPN, тип VPN — на основе маршрута.

   - Создайте второй шлюз виртуальной сети (**азкросс-внетгатевай**) во второй группе ресурсов (**SR-азкросс**).
   - Тип шлюза — VPN, тип VPN — на основе маршрута.

   - Создайте подключение типа "Виртуальная сеть — виртуальная сеть" от первого шлюза виртуальной сети к второму шлюзу виртуальной сети. Укажите общий ключ

   - Создайте подключение типа "Виртуальная сеть — виртуальная сеть" от второго шлюза виртуальной сети к первому шлюзу виртуальной сети. Укажите тот же общий ключ, который указан в предыдущем шаге.

10. На каждом узле кластера откройте порт 59999 (проба работоспособности).

    Выполните следующую команду на каждом узле:

    ```powershell
      netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any
    ```

11. Предложите кластеру прослушивать сообщения проверки работоспособности через порт 59999 и отвечать с узла, который в данный момент владеет этим ресурсом.

    Запустите его один раз с любого узла кластера для каждого кластера.

    В нашем примере необходимо изменить "ИЛБИП" в соответствии со значениями конфигурации. Выполните следующую команду из одного узла **az2az1** / **az2az2**

    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"ProbeFailureThreshold"=5;"EnableDhcp"=0}
    ```

12. Выполните следующую команду из одного узла **azcross1** / **azcross2**
    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.0.0.10" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"ProbeFailureThreshold"=5;"EnableDhcp"=0}
    ```

    Убедитесь, что оба кластера могут подключаться и взаимодействовать друг с другом.

    Либо используйте функцию "подключение к кластеру" в диспетчере отказоустойчивости кластеров для подключения к другому кластеру, либо проверьте, что другой кластер отвечает за один из узлов текущего кластера.

    Из примера мы использовали:
    ```powershell
      Get-Cluster -Name SRAZC1 (ran from azcross1)
    ```
    ```powershell
      Get-Cluster -Name SRAZCross (ran from az2az1)
    ```

13. Создайте облачный следящий сервер для обоих кластеров. Создайте две [учетные записи хранения](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) (**az2azcw**,**азкроссса**) в Azure, по одной для каждого кластера в каждой группе ресурсов (**SR-AZ2AZ**, **SR-азкросс**).

    - Скопируйте имя и ключ учетной записи хранения из "ключи доступа".
    - Создайте облачный следящий сервер из диспетчера отказоустойчивости кластеров и используйте указанные выше имя и ключ учетной записи для ее создания.

14. Выполнение [тестов проверки кластера](../../failover-clustering/create-failover-cluster.md#validate-the-configuration) перед переходом к следующему шагу

15. Запустите Windows PowerShell и используйте командлет [Test-SRTopology](/powershell/module/storagereplica/test-srtopology?view=win10-ps), чтобы определить, все ли требования для реплики хранилища выполнены. Этот командлет можно запустить в режиме быстрой проверки требований или в режиме длительной оценки производительности.

16. Настройка реплики хранилища кластера в кластер.
    Предоставление доступа из одного кластера в другой в обоих направлениях:

    В нашем примере:
    ```powershell
     Grant-SRAccess -ComputerName az2az1 -Cluster SRAZCross
    ```
    Если вы используете Windows Server 2016, выполните также следующую команду:

    ```powershell
     Grant-SRAccess -ComputerName azcross1 -Cluster SRAZC1
    ```

17. Создайте партнерство SR-партнерства для двух кластеров:</ol>

    - Для кластера **SRAZC1**
      - Расположение тома:-c:\ClusterStorage\DataDisk1
      - Расположение журнала:-g:
    - Для кластера **сразкросс**
      - Расположение тома:-К:\клустерстораже\датадисккросс
      - Расположение журнала:-g:

Выполните приведенную ниже команду.

```powershell
PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName SRAZCross -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDiskCross -DestinationLogVolumeName  g:
```
