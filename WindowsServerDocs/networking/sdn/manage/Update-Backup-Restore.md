---
title: Обновление, резервное копирование и восстановление инфраструктуры SDN
description: В этом разделе вы узнаете, как обновить, создать резервную копию и восстановить инфраструктуру SDN.
manager: grcusanz
ms.topic: article
ms.assetid: e9a8f2fd-48fe-4a90-9250-f6b32488b7a4
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/27/2018
ms.openlocfilehash: daca883456a32c707fc2c7b9bfd6193b0d917b58
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942584"
---
# <a name="upgrade-backup-and-restore-sdn-infrastructure"></a>Обновление, резервное копирование и восстановление инфраструктуры SDN

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе вы узнаете, как обновить, создать резервную копию и восстановить инфраструктуру SDN.

## <a name="upgrade-the-sdn-infrastructure"></a>Обновление инфраструктуры SDN
Инфраструктуру SDN можно обновить с Windows Server 2016 до Windows Server 2019. Для порядка обновления выполните ту же последовательность действий, что упоминалось в разделе "Обновление инфраструктуры SDN". Перед обновлением рекомендуется создать резервную копию базы данных сетевого контроллера.

Для компьютеров сетевого контроллера используйте командлет Get-Нетворкконтроллерноде, чтобы проверить состояние узла после завершения обновления. Перед обновлением других узлов убедитесь, что узел возвращен в состояние "Up". После обновления всех узлов сетевого контроллера сетевой контроллер обновляет микрослужбы, работающие в кластере сетевого контроллера, в течение часа. Вы можете активировать немедленное обновление с помощью командлета Update-нетворкконтроллер.

Установите одни и те же обновления Windows на всех компонентах операционной системы системы SDN (программно-определяемая сеть), в том числе:

- В SDN включены узлы Hyper-V
- Виртуальные машины сетевого контроллера
- Виртуальные машины мультиплексора Load Balancer программного обеспечения
- Виртуальные машины шлюза RAS

>[!IMPORTANT]
>При использовании System Center Virtual Manager необходимо обновить его с помощью последних накопительных пакетов обновления.

При обновлении каждого компонента можно использовать любой из стандартных методов установки обновлений Windows. Однако для обеспечения минимального времени простоя рабочих нагрузок и целостности базы данных сетевого контроллера выполните следующие действия.

1. Обновите консоли управления.<p>Установите обновления на каждом из компьютеров, где используется модуль PowerShell сетевого контроллера.  В любом месте, где у вас есть установленная роль RSAT-Нетворкконтроллер. Исключая виртуальные машины сетевого контроллера; Вы обновляете их на следующем шаге.

2. На первой виртуальной машине сетевого контроллера установите все обновления и перезапустите.

3. Прежде чем перейти к следующей виртуальной машине сетевого контроллера, используйте `get-networkcontrollernode` командлет, чтобы проверить состояние обновленного и перезапущенного узла.

4. Во время цикла перезагрузки дождитесь отключения узла сетевого контроллера, а затем снова запустите резервное копирование.<p>После перезагрузки виртуальной машины она может занять несколько минут, прежде чем она вернется в состояние **_up_** . Пример выходных данных см. в разделе

5. Установите обновления на каждую виртуальную машину мультиплексора SLB по одной за раз, чтобы обеспечить непрерывную доступность инфраструктуры подсистемы балансировки нагрузки.

6. Обновите узлы Hyper-V и шлюзы RAS, начиная с узлов, которые содержат шлюзы RAS в режиме **ожидания** .<p>Виртуальные машины шлюза RAS не могут быть перенесены в реальном времени без потери подключений клиентов. Во время цикла обновления необходимо следить за минимальным количеством случаев, когда клиентские подключения отработки отказа переключаются на новый шлюз RAS. При координации обновления узлов и шлюзов RAS каждый клиент отключается один раз в большую часть.

    а. Эвакуировать узел виртуальных машин, которые поддерживают динамическую миграцию.<p>Виртуальные машины шлюза RAS должны остаться на узле.

    b. Установите обновления на каждой виртуальной машине шлюза на этом узле.

    c. Если для обновления требуется перезагрузить виртуальную машину шлюза, Перезагрузите виртуальную машину.

    d. Установите обновления на узле, содержащем только что обновленную виртуальную машину шлюза.

    д) Перезагрузите узел, если это требуется для обновлений.

    е) Повторите эти действия для каждого дополнительного узла, содержащего резервный шлюз.<p>Если резервные шлюзы не сохраняются, выполните те же действия для всех оставшихся узлов.


### <a name="example-use-the-get-networkcontrollernode-cmdlet"></a>Пример. Использование командлета Get-нетворкконтроллерноде

В этом примере выходные данные `get-networkcontrollernode` командлета запускаются в одной из виртуальных машин сетевого контроллера.

Ниже приведены сведения о состоянии узлов, отображаемых в примере выходных данных:

- NCNode1.contoso.com = вниз
- NCNode2.contoso.com = up
- NCNode3.contoso.com = up

>[!IMPORTANT]
>Необходимо подождать несколько минут, пока состояние узла не изменится на до обновления дополнительных узлов _**, по одному**_ за раз.

После обновления всех узлов сетевого контроллера сетевой контроллер обновляет микрослужбы, работающие в кластере сетевого контроллера, в течение часа.

>[!TIP]
>Вы можете активировать немедленное обновление с помощью `update-networkcontroller` командлета.


```Powershell
PS C:\> get-networkcontrollernode
Name            : NCNode1.contoso.com
Server          : NCNode1.Contoso.com
FaultDomain     : fd:/NCNode1.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Down

Name            : NCNode2.Contoso.com
Server          : NCNode2.contoso.com
FaultDomain     : fd:/ NCNode2.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Up

Name            : NCNode3.Contoso.com
Server          : NCNode3.Contoso.com
FaultDomain     : fd:/ NCNode3.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Up
```

### <a name="example-use-the-update-networkcontroller-cmdlet"></a>Пример. Использование командлета Update-нетворкконтроллер
В этом примере показаны выходные данные `update-networkcontroller` командлета для принудительного обновления сетевого контроллера.

>[!IMPORTANT]
>Запустите этот командлет, если больше нет обновлений для установки.


```Powershell
PS C:\> update-networkcontroller
NetworkControllerClusterVersion NetworkControllerVersion
------------------------------- ------------------------
10.1.1                          10.1.15
```

## <a name="backup-the-sdn-infrastructure"></a>Резервное копирование инфраструктуры SDN

Регулярное резервное копирование базы данных сетевого контроллера обеспечивает непрерывность бизнес-процессов в случае аварии или потери данных.  Резервное копирование виртуальных машин сетевого контроллера недостаточно, так как не гарантирует, что сеанс будет продолжаться на нескольких узлах сетевого контроллера.

**Требования.**
* Общий ресурс SMB и учетные данные с разрешениями на чтение и запись для общей папки и файловой системы.
* При необходимости можно использовать групповую управляемую учетную запись службы (GMSA), если сетевой контроллер установлен также с помощью GMSA.

**PROCEDURE**

1. Используйте выбранный метод резервного копирования виртуальной машины или используйте Hyper-V для экспорта копии каждой виртуальной машины сетевого контроллера.<p>Резервное копирование виртуальной машины сетевого контроллера гарантирует наличие необходимых сертификатов для расшифровки базы данных.

2. Если используется System Center Virtual Machine Manager (SCVMM), завершите работу службы SCVMM и создайте ее резервную копию с помощью SQL Server.<p>Целью этого является обеспечение того, что в течение этого времени обновления SCVMM не выполняются, что может привести к несогласованности между резервным копированием сетевого контроллера и SCVMM.

   >[!IMPORTANT]
   >Не перезапускайте службу SCVMM, пока не завершится резервное копирование сетевого контроллера.

3. Создайте резервную копию базы данных сетевого контроллера с помощью `new-networkcontrollerbackup` командлета.

4. Проверьте завершение и успешность резервного копирования с помощью `get-networkcontrollerbackup` командлета.

5. При использовании SCVMM запустите службу SCVMM.



### <a name="example-backing-up-the-network-controller-database"></a>Пример. Резервное копирование базы данных сетевого контроллера

```Powershell
$URI = "https://NC.contoso.com"
$Credential = Get-Credential

# Get or Create Credential object for File share user

$ShareUserResourceId = "BackupUser"

$ShareCredential = Get-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential | Where {$_.ResourceId -eq $ShareUserResourceId }
If ($ShareCredential -eq $null) {
    $CredentialProperties = New-Object Microsoft.Windows.NetworkController.CredentialProperties
    $CredentialProperties.Type = "usernamePassword"
    $CredentialProperties.UserName = "contoso\alyoung"
    $CredentialProperties.Value = "<Password>"

    $ShareCredential = New-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential -Properties $CredentialProperties -ResourceId $ShareUserResourceId -Force
}

# Create backup

$BackupTime = (get-date).ToString("s").Replace(":", "_")

$BackupProperties = New-Object Microsoft.Windows.NetworkController.NetworkControllerBackupProperties
$BackupProperties.BackupPath = "\\fileshare\backups\NetworkController\$BackupTime"
$BackupProperties.Credential = $ShareCredential

$Backup = New-NetworkControllerBackup -ConnectionURI $URI -Credential $Credential -Properties $BackupProperties -ResourceId $BackupTime -Force
```

### <a name="example-checking-the-status-of-a-network-controller-backup-operation"></a>Пример. Проверка состояния операции резервного копирования сетевого контроллера

```Powershell
PS C:\ > Get-NetworkControllerBackup -ConnectionUri $URI -Credential $Credential -ResourceId $Backup.ResourceId
| ConvertTo-JSON -Depth 10
{
    "Tags":  null,
    "ResourceRef":  "/networkControllerBackup/2017-04-25T16_53_13",
    "InstanceId":  "c3ea75ae-2892-4e10-b26c-a2243b755dc8",
    "Etag":  "W/\"0dafea6c-39db-401b-bda5-d2885ded470e\"",
    "ResourceMetadata":  null,
    "ResourceId":  "2017-04-25T16_53_13",
    "Properties":  {
                    "BackupPath":  "\\\\fileshare\backups\NetworkController\\2017-04-25T16_53_13",
                    "ErrorMessage":  "",
                    "FailedResourcesList":  [

                                            ],
                    "SuccessfulResourcesList":  [
                                                    "/networking/v1/credentials/11ebfc10-438c-4a96-a1ee-8a048ce675be",
                                                    "/networking/v1/credentials/41229069-85d4-4352-be85-034d0c5f4658",
                                                    "/networking/v1/credentials/b2a82c93-2583-4a1f-91f8-232b801e11bb",
                                                    "/networking/v1/credentials/BackupUser",
                                                    "/networking/v1/credentials/fd5b1b96-b302-4395-b6cd-ed9703435dd1",
                                                    "/networking/v1/virtualNetworkManager/configuration",
                                                    "/networking/v1/virtualSwitchManager/configuration",
                                                    "/networking/v1/accessControlLists/f8b97a4c-4419-481d-b757-a58483512640",
                                                    "/networking/v1/logicalnetworks/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8",
                                                    "/networking/v1/logicalnetworks/48610528-f40b-4718-938e-99c2be76f1e0",
                                                    "/networking/v1/logicalnetworks/89035b49-1ee3-438a-8d7a-f93cbae40619",
                                                    "/networking/v1/logicalnetworks/a9c8eaa0-519c-4988-acd6-11723e9efae5",
                                                    "/networking/v1/logicalnetworks/d4ea002c-c926-4c57-a178-461d5768c31f",
                                                    "/networking/v1/macPools/11111111-1111-1111-1111-111111111111",
                                                    "/networking/v1/loadBalancerManager/config",
                                                    "/networking/v1/publicIPAddresses/2c502b2d-b39a-4be1-a85a-55ef6a3a9a1d",
                                                    "/networking/v1/GatewayPools/Default",
                                                    "/networking/v1/servers/4c4c4544-0058-5810-8056-b4c04f395931",
                                                    "/networking/v1/servers/4c4c4544-0058-5810-8057-b4c04f395931",
                                                    "/networking/v1/servers/4c4c4544-0058-5910-8056-b4c04f395931",
                                                    "/networking/v1/networkInterfaces/058430d3-af43-4328-a440-56540f41da50",
                                                    "/networking/v1/networkInterfaces/08756090-6d55-4dec-98d5-80c4c5a47db8",
                                                    "/networking/v1/networkInterfaces/2175d74a-aacd-44e2-80d3-03f39ea3bc5d",
                                                    "/networking/v1/networkInterfaces/2400c2c3-2291-4b0b-929c-9bb8da55851a",
                                                    "/networking/v1/networkInterfaces/4c695570-6faa-4e4d-a552-0b36ed3e0962",
                                                    "/networking/v1/networkInterfaces/7e317638-2914-42a8-a2dd-3a6d966028d6",
                                                    "/networking/v1/networkInterfaces/834e3937-f43b-4d3c-88be-d79b04e63bce",
                                                    "/networking/v1/networkInterfaces/9d668fe6-b1c6-48fc-b8b1-b3f98f47d508",
                                                    "/networking/v1/networkInterfaces/ac4650ac-c3ef-4366-96e7-d9488fb661ba",
                                                    "/networking/v1/networkInterfaces/b9f23e35-d79e-495f-a1c9-fa626b85ae13",
                                                    "/networking/v1/networkInterfaces/fdd929f1-f64f-4463-949a-77b67fe6d048",
                                                    "/networking/v1/virtualServers/15a891ee-7509-4e1d-878d-de0cb4fa35fd",
                                                    "/networking/v1/virtualServers/57416993-b410-44fd-9675-727cd4e98930",
                                                    "/networking/v1/virtualServers/5f8aebdc-ee5b-488f-ac44-dd6b57bd316a",
                                                    "/networking/v1/virtualServers/6c812217-5931-43dc-92a8-1da3238da893",
                                                    "/networking/v1/virtualServers/d78b7fa3-812d-4011-9997-aeb5ded2b431",
                                                    "/networking/v1/virtualServers/d90820a5-635b-4016-9d6f-bf3f1e18971d",
                                                    "/networking/v1/loadBalancerMuxes/5f8aebdc-ee5b-488f-ac44-dd6b57bd316a_suffix",
                                                    "/networking/v1/loadBalancerMuxes/d78b7fa3-812d-4011-9997-aeb5ded2b431_suffix",
                                                    "/networking/v1/loadBalancerMuxes/d90820a5-635b-4016-9d6f-bf3f1e18971d_suffix",
                                                    "/networking/v1/Gateways/15a891ee-7509-4e1d-878d-de0cb4fa35fd_suffix",
                                                    "/networking/v1/Gateways/57416993-b410-44fd-9675-727cd4e98930_suffix",
                                                    "/networking/v1/Gateways/6c812217-5931-43dc-92a8-1da3238da893_suffix",
                                                    "/networking/v1/virtualNetworks/b3dbafb9-2655-433d-b47d-a0e0bbac867a",
                                                    "/networking/v1/virtualNetworks/d705968e-2dc2-48f2-a263-76c7892fb143",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.2",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.3",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.4"
                                                ],
                    "InProgressResourcesList":  [

                                                ],
                    "ProvisioningState":  "Succeeded",
                    "Credential":  {
                                        "Tags":  null,
                                        "ResourceRef":  "/credentials/BackupUser",
                                        "InstanceId":  "00000000-0000-0000-0000-000000000000",
                                        "Etag":  null,
                                        "ResourceMetadata":  null,
                                        "ResourceId":  null,
                                        "Properties":  null
                                    }
                }
}
```

## <a name="restore-the-sdn-infrastructure-from-a-backup"></a>Восстановление инфраструктуры SDN из резервной копии

При восстановлении всех необходимых компонентов из резервной копии среда SDN возвращается в рабочее состояние.

>[!IMPORTANT]
>Действия зависят от числа восстановленных компонентов.


1. При необходимости повторно разверните узлы Hyper-V и необходимое хранилище.

2. При необходимости восстановите виртуальные машины сетевого контроллера, виртуальные машины шлюза RAS и виртуальные машины мультиплексора из резервной копии.

3. Завершите работу агента узла NC и агента узла SLB на всех узлах Hyper-V:

    ```
    stop-service slbhostagent

    stop-service nchostagent
    ```

4. Останавливает работу виртуальных машин шлюза RAS.

5. Останавливает виртуальные машины мультиплексора SLB.

6. Восстановите сетевой контроллер с помощью `new-networkcontrollerrestore` командлета.

7. Проверьте **ProvisioningState** восстановления, чтобы узнать, когда восстановление было успешно завершено.

8. При использовании SCVMM восстановите базу данных SCVMM с помощью резервной копии, которая была создана одновременно с резервной копией сетевого контроллера.

9. Если вы хотите восстановить виртуальные машины рабочей нагрузки из резервной копии, сделайте это сейчас.

10. Проверьте работоспособность системы с помощью командлета Debug-нетворкконтроллерконфигуратионстате.

```Powershell
$cred = Get-Credential
Debug-NetworkControllerConfigurationState -NetworkController "https://NC.contoso.com" -Credential $cred

Fetching ResourceType:     accessControlLists
Fetching ResourceType:     servers
Fetching ResourceType:     virtualNetworks
Fetching ResourceType:     networkInterfaces
Fetching ResourceType:     virtualGateways
Fetching ResourceType:     loadbalancerMuxes
Fetching ResourceType:     Gateways
```

### <a name="example-restoring-a-network-controller-database"></a>Пример. Восстановление базы данных сетевого контроллера

```Powershell
$URI = "https://NC.contoso.com"
$Credential = Get-Credential

$ShareUserResourceId = "BackupUser"
$ShareCredential = Get-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential | Where {$_.ResourceId -eq $ShareUserResourceId }

$RestoreProperties = New-Object Microsoft.Windows.NetworkController.NetworkControllerRestoreProperties
$RestoreProperties.RestorePath = "\\fileshare\backups\NetworkController\2017-04-25T16_53_13"
$RestoreProperties.Credential = $ShareCredential

$RestoreTime = (Get-Date).ToString("s").Replace(":", "_")
New-NetworkControllerRestore -ConnectionURI $URI -Credential $Credential -Properties $RestoreProperties -ResourceId $RestoreTime -Force
```

### <a name="example-checking-the-status-of-a-network-controller-database-restore"></a>Пример. Проверка состояния восстановления базы данных сетевого контроллера

```PowerShell
PS C:\ > get-networkcontrollerrestore -connectionuri $uri -credential $cred -ResourceId $restoreTime | convertto-json -depth 10
{
    "Tags":  null,
    "ResourceRef":  "/networkControllerRestore/2017-04-26T15_04_44",
    "InstanceId":  "22edecc8-a613-48ce-a74f-0418789f04f6",
    "Etag":  "W/\"f14f6b84-80a7-4b73-93b5-59a9c4b5d98e\"",
    "ResourceMetadata":  null,
    "ResourceId":  "2017-04-26T15_04_44",
    "Properties":  {
                    "RestorePath":  "\\\\sa18fs\\sa18n22\\NetworkController\\2017-04-25T16_53_13",
                    "ErrorMessage":  null,
                    "FailedResourcesList":  null,
                    "SuccessfulResourcesList":  null,
                    "ProvisioningState":  "Succeeded",
                    "Credential":  null
                }
}
```


Сведения о сообщениях о состоянии конфигурации, которые могут появиться, см. [в статье Устранение неполадок в программном стеке Windows Server 2016](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack).