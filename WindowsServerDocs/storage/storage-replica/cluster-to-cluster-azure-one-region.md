---
title: Кластер в реплику хранилища кластера в том же регионе Azure
description: Репликация кластера в хранилище кластера в том же регионе Azure
author: arduppal
ms.author: arduppal
ms.date: 04/26/2019
ms.topic: article
manager: mchad
ms.openlocfilehash: d5c200d649bfa62314eca26cee3f5fe8601895c3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950488"
---
# <a name="cluster-to-cluster-storage-replica-within-the-same-region-in-azure"></a>Кластер в реплику хранилища кластера в том же регионе Azure

> Применяется к: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)

Вы можете настроить репликацию кластера для репликации хранилища кластера в том же регионе Azure. В приведенных ниже примерах мы используем кластер из двух узлов, но Реплика хранилища кластера не ограничена кластером из двух узлов. На рисунке ниже представлен кластер прямого дискового пространства с двумя узлами, который может взаимодействовать друг с другом, находиться в одном домене и в одном регионе.

Просмотрите видео ниже, чтобы ознакомиться с полным пошаговым процессом.

Часть 1
> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE26f2Y]

Часть 2
> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE269Pq]

![Схема архитектуры, предоставляющая реплику хранилища кластера в кластер в Azure в том же регионе.](media/Cluster-to-cluster-azure-one-region/architecture.png)
> [!IMPORTANT]
> Все примеры, на которые указывают ссылки, относятся к иллюстрации выше.

1. Создайте [группу ресурсов](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup) в портал Azure в регионе (**SR-AZ2AZ** в **западной части США 2**).
2. Создайте две группы [доступности](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM) в группе ресурсов (**SR-AZ2AZ**), созданной выше, по одной для каждого кластера.
    а. Группа доступности (**az2azAS1**) b. Группа доступности (**az2azAS2**)
3. Создайте [виртуальную сеть](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**az2az-vnet**) в ранее созданной группе ресурсов (**SR-az2az**), имеющую по крайней мере одну подсеть.
4. Создайте [группу безопасности сети](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**az2az-NSG**) и добавьте одно правило безопасности для входящего трафика для RDP: 3389. Вы можете удалить это правило после завершения установки.
5. Создайте [виртуальные машины](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM) Windows Server в ранее созданной группе ресурсов (**SR-AZ2AZ**). Используйте ранее созданную виртуальную сеть (**az2az-vnet**) и группу безопасности сети (**az2az-NSG**).

   Контроллер домена (**az2azDC**). Вы можете создать третью группу доступности для контроллера домена или добавить контроллер домена в одну из двух групп доступности. Если вы добавляете это в группу доступности, созданную для двух кластеров, назначьте ей Стандартный общедоступный IP-адрес во время создания виртуальной машины.
   - Установите службу домен Active Directory.
   - Создание домена (Contoso.com)
   - Создание пользователя с правами администратора (contosoadmin)
   - Создайте две виртуальные машины (**az2az1**, **az2az2**) в первой группе доступности (**az2azAS1**). Назначьте стандартные общедоступные IP-адреса каждой виртуальной машине во время создания.
   - Добавление на каждый компьютер как минимум 2 управляемых дисков
   - Установка компонента отказоустойчивой кластеризации и реплики хранилища
   - Создайте две виртуальные машины (**az2az3**, **az2az4**) во второй группе доступности (**az2azAS2**). Назначьте стандартные общедоступные IP-адреса каждой виртуальной машине во время создания.
   - Добавьте на каждый компьютер не менее 2 управляемых дисков.
   - Установите компонент отказоустойчивой кластеризации и реплики хранилища.

6. Подключите все узлы к домену и предоставьте права администратора для ранее созданного пользователя.

7. Измените DNS-сервер виртуальной сети на частный IP-адрес контроллера домена.
8. В нашем примере контроллер домена **az2azDC** имеет частный IP-адрес (10.3.0.8). В виртуальной сети (**az2az-vnet**) измените DNS-сервер 10.3.0.8. Подключите все узлы к "Contoso.com" и предоставьте права администратора для "contosoadmin".
   - Войдите как contosoadmin со всех узлов.

9. Создайте кластеры (**SRAZC1**, **SRAZC2**).
   Ниже приведены команды PowerShell для нашего примера.
   ```PowerShell
    New-Cluster -Name SRAZC1 -Node az2az1,az2az2 –StaticAddress 10.3.0.100
   ```
   ```PowerShell
    New-Cluster -Name SRAZC2 -Node az2az3,az2az4 –StaticAddress 10.3.0.101
   ```
10. Включить локальные дисковые пространства
    ```PowerShell
    Enable-clusterS2D
    ```

    Для каждого кластера создайте виртуальный диск и том. Один для данных, а другой для журнала.

11. Создайте внутренний [Load Balancer](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM) SKU "Стандартный" для каждого кластера (**azlbr1**,**azlbr2**).

    Укажите IP-адрес кластера в виде статического частного IP-адреса для балансировщика нагрузки.
    - azlbr1 => интерфейсный IP-адрес: 10.3.0.100 (выбор неиспользуемого IP-адреса из подсети виртуальной сети (**az2az-vnet**))
    - Создайте серверный пул для каждой подсистемы балансировки нагрузки. Добавьте связанные узлы кластера.
    - Создание проверки работоспособности: порт 59999
    - Создать правило балансировки нагрузки: разрешить порты с высоким уровнем доступности с включенным плавающим IP-адресом.

    Укажите IP-адрес кластера в виде статического частного IP-адреса для балансировщика нагрузки.
    - azlbr2 => интерфейсный IP-адрес: 10.3.0.101 (выбор неиспользуемого IP-адреса из подсети виртуальной сети (**az2az-vnet**))
    - Создайте серверный пул для каждой подсистемы балансировки нагрузки. Добавьте связанные узлы кластера.
    - Создание проверки работоспособности: порт 59999
    - Создать правило балансировки нагрузки: разрешить порты с высоким уровнем доступности с включенным плавающим IP-адресом.

12. На каждом узле кластера откройте порт 59999 (проба работоспособности).

    Выполните следующую команду на каждом узле:
    ```PowerShell
    netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any
    ```
13. Предложите кластеру прослушивать сообщения проверки работоспособности через порт 59999 и отвечать с узла, который в данный момент владеет этим ресурсом.
    Запустите его один раз с любого узла кластера для каждого кластера.

    В нашем примере необходимо изменить "ИЛБИП" в соответствии со значениями конфигурации. Выполните следующую команду из одного узла **az2az1** / **az2az2**:

    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"ProbeFailureThreshold"=5;"EnableDhcp"=0}
    ```

14. Выполните следующую команду из одного узла **az2az3** / **az2az4**.

    ```PowerShell
    $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
    $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
    $ILBIP = "10.3.0.101" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
    [int]$ProbePort = 59999
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"ProbeFailureThreshold"=5;"EnableDhcp"=0}
    ```
    Убедитесь, что оба кластера могут подключаться и взаимодействовать друг с другом.

    Либо используйте функцию "подключение к кластеру" в диспетчере отказоустойчивости кластеров для подключения к другому кластеру, либо проверьте, что другой кластер отвечает за один из узлов текущего кластера.

    ```PowerShell
     Get-Cluster -Name SRAZC1 (ran from az2az3)
    ```
    ```PowerShell
     Get-Cluster -Name SRAZC2 (ran from az2az1)
    ```

15. Создайте Cloud следящих серверов для обоих кластеров. Создайте две [учетные записи хранения](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) (**az2azcw**, **az2azcw2**) в Azure One для каждого кластера в одной группе ресурсов (**SR-AZ2AZ**).

    - Скопируйте имя и ключ учетной записи хранения из "ключи доступа".
    - Создайте облачный следящий сервер из диспетчера отказоустойчивости кластеров и используйте указанные выше имя и ключ учетной записи для ее создания.

16. Выполните [проверочные тесты кластера](../../failover-clustering/create-failover-cluster.md#validate-the-configuration) , прежде чем переходить к следующему шагу.

17. Запустите Windows PowerShell и используйте командлет [Test-SRTopology](/powershell/module/storagereplica/test-srtopology?view=win10-ps), чтобы определить, все ли требования для реплики хранилища выполнены. Командлет можно использовать в режиме "только требования" для быстрой проверки, а также для длительного режима оценки производительности.

18. Настройка реплики хранилища кластера в кластер.

    Предоставление доступа из одного кластера в другой в обоих направлениях:

    Пример.

    ```PowerShell
      Grant-SRAccess -ComputerName az2az1 -Cluster SRAZC2
    ```
    Если вы используете Windows Server 2016, то также выполните следующую команду:

    ```PowerShell
      Grant-SRAccess -ComputerName az2az3 -Cluster SRAZC1
    ```

19. Создайте Српартнершип для кластеров:</ol>

    - Для кластера **SRAZC1**.
    - Расположение тома:-c:\ClusterStorage\DataDisk1
    - Расположение журнала:-g:
    - Для кластера **SRAZC2**
    - Расположение тома:-c:\ClusterStorage\DataDisk2
    - Расположение журнала:-g:

Выполните следующую команду:

```PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName **SRAZC2** -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDisk2 -DestinationLogVolumeName  g:
```
