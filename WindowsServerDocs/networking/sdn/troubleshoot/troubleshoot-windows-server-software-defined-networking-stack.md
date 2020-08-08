---
title: Диагностика стека программно-конфигурируемой сети Windows Server
description: В этом руководство по Windows Server изучаются распространенные ошибки и случаи сбоя программно-определяемой сети (SDN), а также описывается процесс устранения неполадок, использующий доступные средства диагностики.
manager: grcusanz
ms.topic: article
ms.assetid: 9be83ed2-9e62-49e8-88e7-f52d3449aac5
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/14/2018
ms.openlocfilehash: 87972f9a0d83a4b7f192e2fe0f751ee66c599044
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955921"
---
# <a name="troubleshoot-the-windows-server-software-defined-networking-stack"></a>Диагностика стека программно-конфигурируемой сети Windows Server

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом руководство рассматриваются распространенные ошибки и случаи сбоя программно-определяемой сети (SDN), а также описывается процесс устранения неполадок, использующий доступные средства диагностики.

Дополнительные сведения о программно определяемой сети Майкрософт см. в разделе [программно определяемая сеть](../../sdn/Software-Defined-Networking--SDN-.md).

## <a name="error-types"></a>Типы ошибок
В следующем списке представлен класс проблем, наиболее часто возникающих при использовании виртуализации сети Hyper-V (HNVv1) в Windows Server 2012 R2 из рабочих развертываний на рынке, и совпадают различные типы проблем, возникающих в Windows Server 2016 HNVv2 с новым стеком программно-определяемой сети (SDN).

Большинство ошибок можно классифицировать в небольшой набор классов:
* **Недопустимая или неподдерживаемая конфигурация** Пользователь неправильно вызывает API обмена или имеет недопустимую политику.

* **Ошибка в приложении политики** Политика сетевого контроллера не доставляется на узел Hyper-V, значительно отложена и (или) не обновлена на всех узлах Hyper-V (например, после динамическая миграция).
* Отклонение **конфигурации или ошибка программного обеспечения** Проблемы с путями с данными, приводящие к потере пакетов.

* **Внешняя ошибка, связанная с сетевым адаптером, драйверами или структурой сети ундерлай** Неправильно настроенные разгрузки задач (например, VMQ) или ундерлай Network Fabric (например, MTU)

  В этом руководство по устранению неполадок изучаются все эти категории ошибок и приводятся рекомендации и средства диагностики, доступные для выявления и исправления ошибок.

## <a name="diagnostic-tools"></a>Диагностические средства

Прежде чем обсуждать рабочие процессы устранения неполадок для каждого из этих типов ошибок, давайте рассмотрим доступные средства диагностики.

Чтобы использовать средства диагностики сетевого контроллера (Control-Path), необходимо сначала установить компонент RSAT-Нетворкконтроллер и импортировать ``NetworkControllerDiagnostics`` модуль:

```powershell
Add-WindowsFeature RSAT-NetworkController -IncludeManagementTools
Import-Module NetworkControllerDiagnostics
```

Чтобы использовать средства диагностики диагностики HNV (Data-Path), необходимо импортировать ``HNVDiagnostics`` модуль:

```powershell
# Assumes RSAT-NetworkController feature has already been installed
Import-Module hnvdiagnostics
```

### <a name="network-controller-diagnostics"></a>Диагностика сетевого контроллера
Эти командлеты описаны на сайте TechNet в [разделе Командлет диагностики сетевого контроллера](https://docs.microsoft.com/powershell/module/networkcontrollerdiagnostics/). Они помогают выявление проблем с согласованностью сетевых политик в узлах сетевого контроллера, а также между сетевым контроллером и агентами узла NC, запущенными на узлах Hyper-V.

 Командлеты _Debug-сервицефабрикнодестатус_ и _Get-нетворкконтроллерреплика_ должны запускаться с одной из виртуальных машин узла сетевого контроллера. Все остальные командлеты диагностики NC можно запускать с любого узла, который имеет подключение к сетевому контроллеру и находится в группе безопасности управления сетевым контроллером (Kerberos) или имеет доступ к сертификату X. 509 для управления сетевым контроллером.

### <a name="hyper-v-host-diagnostics"></a>Диагностика узлов Hyper-V
Эти командлеты описаны на сайте TechNet в [разделе командлета диагностики виртуализации сети Hyper-V (HNV)](https://docs.microsoft.com/powershell/module/hnvdiagnostics/). Они помогают выявление проблем в пути передачи данных между виртуальными машинами клиента (Восток/Западная) и входящим трафиком через виртуальный IP-адрес SLB (Север/Юг).

Для всех локальных тестов, которые можно запускать с любого узла Hyper-V, поддерживаются _Отладка-виртуалмачинекуеуеоператион_, Get- _кустомеррауте_ _, Get-_ _провидераддресс_, Get- _вмнетворкадаптерпортид_, _Get-VMSwitchExternalPortId_и _Test-EncapOverheadSettings_ . Другие командлеты вызывают проверку пути к данным через сетевой контроллер, поэтому требуется доступ к сетевому контроллеру как дескриед выше.

### <a name="github"></a>GitHub
[Репозиторий GitHub Microsoft/Sdn](https://github.com/microsoft/sdn) содержит ряд примеров сценариев и рабочих процессов, которые создаются на основе этих командлетов. В частности, диагностические сценарии можно найти в папке [Diagnostics](https://github.com/Microsoft/sdn/diagnostics) . Помогите нам участвовать в этих сценариях, отправив запросы на вытягивание.

## <a name="troubleshooting-workflows-and-guides"></a>Устранение неполадок рабочих процессов и руководств

### <a name="hoster-validate-system-health"></a>Поставщика услуг размещения Проверка работоспособности системы
В некоторых ресурсах сетевого контроллера имеется внедренный ресурс с именем _Configuration State_ . Состояние конфигурации предоставляет сведения о работоспособности системы, включая согласованность конфигурации сетевого контроллера и фактическое (запущенное) состояние на узлах Hyper-V.

Чтобы проверить состояние конфигурации, выполните следующую команду с любого узла Hyper-V с подключением к сетевому контроллеру.

>[!NOTE]
>Значение параметра *нетворкконтроллер* должно быть либо полным доменным именем, либо IP-адресом, исходя из имени субъекта сертификата X. 509 >, созданного для сетевого контроллера.
>
>Параметр *Credential* необходимо указывать, только если сетевой контроллер использует проверку подлинности Kerberos (обычно в развертываниях VMM). Учетные данные должны быть заданы для пользователя, который находится в группе безопасности "Управление сетевым контроллером".

```
Debug-NetworkControllerConfigurationState -NetworkController <FQDN or NC IP> [-Credential <PS Credential>]

# Healthy State Example - no status reported
$cred = Get-Credential
Debug-NetworkControllerConfigurationState -NetworkController 10.127.132.211 -Credential $cred

Fetching ResourceType:     accessControlLists
Fetching ResourceType:     servers
Fetching ResourceType:     virtualNetworks
Fetching ResourceType:     networkInterfaces
Fetching ResourceType:     virtualGateways
Fetching ResourceType:     loadbalancerMuxes
Fetching ResourceType:     Gateways
```

Ниже приведен пример сообщения о состоянии конфигурации.

```
Fetching ResourceType:     servers
---------------------------------------------------------------------------------------------------------
ResourcePath:     https://10.127.132.211/Networking/v1/servers/4c4c4544-0056-4b10-8058-b8c04f395931
Status:           Warning

Source:           SoftwareLoadBalancerManager
Code:             HostNotConnectedToController
Message:          Host is not Connected.
----------------------------------------------------------------------------------------------------------
```

>[!NOTE]
> В системе имеется ошибка, в которой ресурсы сетевого интерфейса для транзитного сетевого адаптера виртуальной машины мультиплексора SLB находятся в состоянии сбоя с ошибкой "виртуальный коммутатор — узел не подключен к контроллеру". Эту ошибку можно спокойно проигнорировать, если в IP-конфигурации в ресурсе NIC виртуальной машины задан IP-адрес из пула IP-адресов транзитной логической сети.
> В системе есть вторая ошибка, в которой ресурсы сетевого интерфейса для сетевых адаптеров виртуальных машин поставщика HNV шлюза находятся в состоянии сбоя с ошибкой "Virtual Switch-Портблоккед". Эту ошибку также можно спокойно проигнорировать, если IP-конфигурация в ресурсе NIC виртуальной машины имеет значение null (по шаблону).

В таблице ниже приведен список кодов ошибок, сообщений и дальнейших действий, которые необходимо выполнить в зависимости от состояния конфигурации.

| **Код** | **Message** | **Действие** |
|--|--|--|
| Неизвестно | Неизвестная ошибка |  |
| хостунреачабле | Хост-компьютер недоступен | Проверка сетевого подключения управления между сетевым контроллером и узлом |
| паипаддрессексхаустед | IP-адреса PA исчерпаны | Увеличение размера пула IP-адресов для логической подсети поставщика HNV |
| памакаддрессексхаустед | Mac-адреса PA исчерпаны | Увеличение диапазона пула MAC-адресов |
| пааддрессконфигуратионфаилуре | Не удалось подключить адреса PA к узлу | Проверьте сетевое соединение управления между сетевым контроллером и узлом. |
| цертификатеноттрустед | Сертификат не является доверенным | Исправьте сертификаты, используемые для связи с узлом. |
| цертификатенотаусоризед | Сертификат не является полномочным | Исправьте сертификаты, используемые для связи с узлом. |
| полициконфигуратионфаилуреонвфп | Сбой при настройке политик VFP | Это сбой среды выполнения.  Не существует определенной обработки. Собирайте журналы. |
| полициконфигуратионфаилуре | Сбой при принудительной отправке политик на узлы из-за сбоев связи или других ошибок в Нетворкконтроллер. | Нет определенных действий.  Это происходит из-за сбоя обработки состояния цели в модулях сетевого контроллера. Собирайте журналы. |
| хостнотконнектедтоконтроллер | Узел еще не подключен к сетевому контроллеру | Профиль порта не применяется на узле, или узел недоступен из сетевого контроллера. Проверка того, что раздел реестра HostID соответствует ИДЕНТИФИКАТОРу экземпляра ресурса сервера |
| мултиплевфпенабледсвитчес | На узле есть несколько переключателей с поддержкой VFp. | Удалите один из переключателей, так как агент узла сетевого контроллера поддерживает только один vSwitch с включенным расширением VFP. |
| полициконфигуратионфаилуре | Не удалось принудительно отправить политики виртуальной сети для Вмник из-за ошибок сертификата или ошибок подключения. | Проверьте, развернуты ли правильные сертификаты (имя субъекта сертификата должно соответствовать полному доменному имени узла). Также проверьте подключение узла к сетевому контроллеру. |
| полициконфигуратионфаилуре | Не удалось принудительно отправить политики vSwitch для Вмник из-за ошибок сертификата или ошибок подключения. | Проверьте, развернуты ли правильные сертификаты (имя субъекта сертификата должно соответствовать полному доменному имени узла). Также проверьте подключение узла к сетевому контроллеру. |
| полициконфигуратионфаилуре | Не удалось принудительно отправить политики брандмауэра для Вмник из-за ошибок сертификата или ошибок подключения. | Проверьте, развернуты ли правильные сертификаты (имя субъекта сертификата должно соответствовать полному доменному имени узла). Также проверьте подключение узла к сетевому контроллеру. |
| дистрибутедраутерконфигуратионфаилуре | Не удалось настроить параметры распределенного маршрутизатора на узле vNic | Ошибка стека TCPIP. Может потребоваться очистка узла vNIC и сервера аварийного восстановления на сервере, на котором была обнаружена эта ошибка. |
| дхкпаддрессаллокатионфаилуре | Сбой выделения адреса DHCP для Вмник | Проверьте, настроен ли атрибут статического IP-адреса в ресурсе сетевой карты. |
| цертификатеноттрустед<br>цертификатенотаусоризед | Не удалось подключиться к мультиплексору из-за ошибок сети или сертификата | Проверьте числовой код, указанный в коде сообщения об ошибке: это соответствует коду ошибки Winsock. Ошибки сертификата детализированы (например, сертификат не может быть проверен, сертификат не прошел проверку и т. д.). |
| хостунреачабле | МУЛЬТИПЛЕКСОР находится в неработоспособном состоянии (общий случай — Бгпраутер DISCONNECTED) | Одноранговый узел BGP на RRAS (виртуальная машина BGP) или коммутатор верхнего уровня (ToR) недоступен или не был успешно установлен в пиринг. Проверьте параметры BGP для ресурса мультиплексора Load Balancer программного обеспечения и узла BGP (ToR или виртуальная машина RRAS). |
| хостнотконнектедтоконтроллер | Агент узла SLB не подключен | Убедитесь, что служба агента узла SLB запущена; В разделе журналы агента узла SLB (автоматический запуск) приведены причины, по которым в случае, если сертификат, предоставленный агентом узла под состоянием "выполняется" (NC) отклонен, будет показывать сведения об особенностях |
| портблоккед | Порт VFP заблокирован из-за отсутствия политик виртуальной сети и списка управления доступом | Проверьте наличие других ошибок, которые могут привести к тому, что политики не будут настроены. |
| Перегрузка | МУЛЬТИПЛЕКСОР подсистемы балансировки нагрузки перегружен | Проблемы с производительностью МУЛЬТИПЛЕКСОРа |
| раутепубликатионфаилуре | МУЛЬТИПЛЕКСОР подсистемы балансировки нагрузки не подключен к маршрутизатору BGP | Проверьте, есть ли у МУЛЬТИПЛЕКСОРа связь с маршрутизаторами BGP и правильно ли настроен пиринг BGP. |
| виртуалсерверунреачабле | МУЛЬТИПЛЕКСОР подсистемы балансировки нагрузки не подключен к диспетчеру SLB | Проверка подключения между SLBM и МУЛЬТИПЛЕКСОРом |
| косконфигуратионфаилуре | Не удалось настроить политики качества обслуживания | Проверьте, доступна ли достаточная пропускная способность для всех виртуальных машин, если используется резервирование QOS. |

#### <a name="check-network-connectivity-between-the-network-controller-and-hyper-v-host-nc-host-agent-service"></a>Проверка сетевого подключения между сетевым контроллером и узлом Hyper-V (служба агента узла NC)
Выполните следующую команду *netstat* , чтобы проверить наличие трех установленных подключений между агентом узла NC и узлами сетевого контроллера и одним СОКЕТом прослушивания на узле Hyper-V.
- ПРОСЛУШИВАНИе порта TCP: 6640 на узле Hyper-V (служба агента узла NC)
- Два установленных подключения от IP-адреса узла Hyper-V через порт 6640 к IP-адресу узла NC на временных портах (> 32000)
- Одно установленное подключение с IP-адреса узла Hyper-V на временных портах к IP-адресу сети сетевого контроллера по порту 6640

>[!NOTE]
>На узле Hyper-V может быть только два установленных подключения, если на этом узле не развернуты виртуальные машины клиента.

```
netstat -anp tcp |findstr 6640

# Successful output
  TCP    0.0.0.0:6640           0.0.0.0:0              LISTENING
  TCP    10.127.132.153:6640    10.127.132.213:50095   ESTABLISHED
  TCP    10.127.132.153:6640    10.127.132.214:62514   ESTABLISHED
  TCP    10.127.132.153:50023   10.127.132.211:6640    ESTABLISHED
```

#### <a name="check-host-agent-services"></a>Проверка служб агента узла
Сетевой контроллер взаимодействует с двумя службами агента узла на узлах Hyper-V: агент узла SLB и агент узла NC. Возможно, одна или обе службы не работают. Проверьте их состояние и перезапустите, если они не запущены.

```
Get-Service SlbHostAgent
Get-Service NcHostAgent

# (Re)start requires -Force flag
Start-Service NcHostAgent -Force
Start-Service SlbHostAgent -Force
```

#### <a name="check-health-of-network-controller"></a>Проверка работоспособности сетевого контроллера
Если нет трех установленных подключений или сетевой контроллер не отвечает, убедитесь, что все узлы и модули службы работают и работают с помощью следующих командлетов.

```none
# Prints a DIFF state (status is automatically updated if state is changed) of a particular service module replica
Debug-ServiceFabricNodeStatus [-ServiceTypeName] <Service Module>

```
Модули службы сетевого контроллера:
- контроллерсервице
- аписервице
- слбманажерсервице
- сервицеинсертион
- фиреваллсервице
- всвитчсервице
- GatewayManager
- фнмсервице
- хелперсервице
- UpdateService
```

Check that ReplicaStatus is **Ready** and HealthState is **Ok**.

In a production deployment is with a multi-node Network Controller, you can also check which node each service is primary on and its individual replica status.

```powershell
Get-NetworkControllerReplica

# Sample Output for the API service module
Replicas for service: ApiService

ReplicaRole   : Primary
NodeName      : SA18N30NC3.sa18.nttest.microsoft.com
ReplicaStatus : Ready
```

Убедитесь, что состояние реплики готово для каждой службы.

#### <a name="check-for-corresponding-hostids-and-certificates-between-network-controller-and-each-hyper-v-host"></a>Проверьте наличие соответствующих Хостидс и сертификатов между сетевым контроллером и каждым узлом Hyper-V.
На узле Hyper-V выполните следующие команды, чтобы проверить, соответствует ли HostID идентификатору экземпляра ресурса сервера на сетевом контроллере.

```powershell
Get-ItemProperty "hklm:\system\currentcontrolset\services\nchostagent\parameters" -Name HostId |fl HostId

HostId : **162cd2c8-08d4-4298-8cb4-10c2977e3cfe**

Get-NetworkControllerServer -ConnectionUri $uri |where { $_.InstanceId -eq "162cd2c8-08d4-4298-8cb4-10c2977e3cfe"}

Tags             :
ResourceRef      : /servers/4c4c4544-0056-4a10-8059-b8c04f395931
InstanceId       : **162cd2c8-08d4-4298-8cb4-10c2977e3cfe**
Etag             : W/"50f89b08-215c-495d-8505-0776baab9cb3"
ResourceMetadata : Microsoft.Windows.NetworkController.ResourceMetadata
ResourceId       : 4c4c4544-0056-4a10-8059-b8c04f395931
Properties       : Microsoft.Windows.NetworkController.ServerProperties
```

*Исправление* При использовании скриптов Сднекспресс или ручного развертывания Обновите ключ HostId в реестре в соответствии с идентификатором экземпляра ресурса сервера. Перезапустите агент узла сетевого контроллера на узле Hyper-V (физический сервер), если используется VMM, удалите сервер Hyper-V из VMM и удалите раздел реестра HostId. Затем повторно добавьте сервер с помощью VMM.

Убедитесь, что отпечатки сертификатов X. 509, используемых узлом Hyper-V (имя узла будет совпадать с именем субъекта сертификата) для (Подсистемамми) связи между узлом Hyper-V (служба агента узла NC) и узлами сетевого контроллера, совпадают. Также убедитесь, что в сертификате RESTFUL сетевого контроллера есть имя субъекта *CN <FQDN or IP> =*.

```
# On Hyper-V Host
dir cert:\\localmachine\my

Thumbprint                                Subject
----------                                -------
2A3A674D07D8D7AE11EBDAC25B86441D68D774F9  CN=SA18n30-4.sa18.nttest.microsoft.com
...

dir cert:\\localmachine\root

Thumbprint                                Subject
----------                                -------
30674C020268AA4E40FD6817BA6966531FB9ADA4  CN=10.127.132.211 **# NC REST IP ADDRESS**

# On Network Controller Node VM
dir cert:\\localmachine\root

Thumbprint                                Subject
----------                                -------
2A3A674D07D8D7AE11EBDAC25B86441D68D774F9  CN=SA18n30-4.sa18.nttest.microsoft.com
30674C020268AA4E40FD6817BA6966531FB9ADA4  CN=10.127.132.211 **# NC REST IP ADDRESS**
...
```

Кроме того, можно проверить следующие параметры каждого сертификата, чтобы убедиться, что имя субъекта является ожидаемым (имя узла или полное доменное имя или IP-адрес для остальных узлов), срок действия сертификата еще не истек и все центры сертификации в цепочке сертификатов включены в доверенный корневой центр сертификации.

- Имя субъекта
- Срок действия
- Доверенный корневой центр

*Исправление* Если на узле Hyper-V несколько сертификатов имеют одно и то же имя субъекта, агент узла сетевого контроллера будет случайным образом выбрать один из них для сетевого контроллера. Это может не соответствовать отпечатку ресурса сервера, известного сетевому контроллеру. В этом случае удалите один из сертификатов с тем же именем субъекта на узле Hyper-V, а затем повторно запустите службу агента узла сетевого контроллера. Если подключение по-прежнему не удается выполнить, удалите другой сертификат с тем же именем субъекта на узле Hyper-V и удалите соответствующий ресурс сервера в VMM. Затем повторно создайте ресурс сервера в VMM, который создаст новый сертификат X. 509 и установит его на узле Hyper-V.

#### <a name="check-the-slb-configuration-state"></a>Проверка состояния конфигурации SLB
Состояние конфигурации SLB можно определить как часть выходных данных для командлета Debug-Нетворкконтроллер. Этот командлет также выводит текущий набор ресурсов сетевого контроллера в JSON-файлах, все конфигурации IP из каждой политики узла Hyper-V (сервера) и локальной сети из таблиц базы данных агента узла.

По умолчанию будут собираться дополнительные трассировки. Чтобы не выполнять накопление трассировок, добавьте параметр-Инклудетрацес: $false.

```
Debug-NetworkController -NetworkController <FQDN or IP> [-Credential <PS Credential>] [-IncludeTraces:$false]

# Don't collect traces
$cred = Get-Credential
Debug-NetworkController -NetworkController 10.127.132.211 -Credential $cred -IncludeTraces:$false

Transcript started, output file is C:\\NCDiagnostics.log
Collecting Diagnostics data from NC Nodes
```

>[!NOTE]
>Расположением выходных данных по умолчанию будет <working_directory> каталог \Нкдиагностикс\. Выходной каталог по умолчанию можно изменить с помощью `-OutputDirectory` параметра.

Сведения о состоянии конфигурации SLB можно найти в _diagnostics-slbstateResults.Js_ файле в этом каталоге.

Этот файл JSON можно разделить на следующие разделы:

 * Fabric
   * Слбмвипс. в этом разделе приводится IP-адрес виртуального сетевого адреса диспетчера SLB, который используется сетевым контроллером для кудинате конфигурации и работоспособности агентов узлов SLB мультиплексоров и SLB.
   * Муксстате — в этом разделе перечислены по одному значению для каждого развернутого мультиплексора SLB, который обеспечивает состояние мультиплексора.
   * Настройка маршрутизатора. в этом разделе перечислены номер автономной системы (ASN) вышестоящего маршрутизатора, IP-адрес транзитного маршрута и идентификатор. В нем также будет перечисляться IP-адрес SLB мультиплексоров ASN и транзитный.
   * Сведения о подключенном узле. в этом разделе перечислены IP-адреса всех узлов Hyper-V, доступных для выполнения рабочих нагрузок с балансировкой нагрузки.
   * Диапазоны виртуальных IP-адресов. в этом разделе перечислены диапазоны пула общедоступных и частных ВИРТУАЛЬНЫХ IP-адресов. Виртуальный IP-адрес SLBM будет добавлен в качестве выделенного в один из этих диапазонов.
   * Маршруты мультиплексора. в этом разделе приводится список по одному значению для каждого развернутого мультиплексора SLB, содержащего все объявления маршрутов для этого конкретного мультиплексора.
 * Клиент
   * Випконсолидатедстате. в этом разделе перечисляются сведения о состоянии подключения для каждого виртуального IP-адреса клиента, включая объявленный префикс маршрута, узлы и конечные точки DIP.

> [!NOTE]
> Состояние SLB можно проверить непосредственно с помощью скрипта [думпслбрестстате](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) , доступного в [репозитории GitHub Microsoft Sdn](https://github.com/microsoft/sdn).

#### <a name="gateway-validation"></a>Проверка шлюза

**Из сетевого контроллера:**

```powershell
Get-NetworkControllerLogicalNetwork
Get-NetworkControllerPublicIPAddress
Get-NetworkControllerGatewayPool
Get-NetworkControllerGateway
Get-NetworkControllerVirtualGateway
Get-NetworkControllerNetworkInterface
```

**Из виртуальной машины шлюза:**

```powershell
Ipconfig /allcompartments /all
Get-NetRoute -IncludeAllCompartments -AddressFamily
Get-NetBgpRouter
Get-NetBgpRouter | Get-BgpPeer
Get-NetBgpRouter | Get-BgpRouteInformation
```

**Переключение с верхней части стойки (ToR):**

`sh ip bgp summary (for 3rd party BGP Routers)`

**Маршрутизатор Windows BGP**

```powershell
Get-BgpRouter
Get-BgpPeer
Get-BgpRouteInformation
```

В дополнение к ним, от проблем, которые мы видели до сих пор (особенно при развертывании на основе Сднекспресс), наиболее распространенной причиной, по которой для секции клиента не настраивается на виртуальных машинах GW, является тот факт, что емкость GW в FabricConfig.psd1 меньше по сравнению с тем, что люди пытаются назначить сетевому подключению (туннели S2S) в TenantConfig.psd1. Это можно легко проверить, сравнив выходные данные следующих команд:

```powershell
PS > (Get-NetworkControllerGatewayPool -ConnectionUri $uri).properties.Capacity
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").properties.OutboundKiloBitsPerSecond
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").property
```

### <a name="hoster-validate-data-plane"></a>Поставщика услуг размещения Проверить плоскость данных
После развертывания сетевого контроллера были созданы виртуальные сети и подсети клиента, а виртуальные сети подключены к виртуальным подсетям. поставщик услуг размещения может выполнять дополнительные тесты на уровне структуры для проверки возможности подключения клиента.

#### <a name="check-hnv-provider-logical-network-connectivity"></a>Проверка подключения к логической сети поставщика HNV
После подключения первой гостевой виртуальной машины, запущенной на узле Hyper-V к виртуальной сети клиента, сетевой контроллер присвоит узлу Hyper-V два IP-адреса поставщика HNV (IP-адреса PA). Эти IP-адреса будут поступать из пула HNVов логической сети поставщика услуг и управляться сетевым контроллером.  Чтобы узнать, что такое два IP-адреса HNV

```powershell
PS > Get-ProviderAddress

# Sample Output
ProviderAddress : 10.10.182.66
MAC Address     : 40-1D-D8-B7-1C-04
Subnet Mask     : 255.255.255.128
Default Gateway : 10.10.182.1
VLAN            : VLAN11

ProviderAddress : 10.10.182.67
MAC Address     : 40-1D-D8-B7-1C-05
Subnet Mask     : 255.255.255.128
Default Gateway : 10.10.182.1
VLAN            : VLAN11
```

Эти IP-адреса поставщика HNV (PA) назначаются адаптерам Ethernet, созданным в отдельном сетевом сегменте TCPIP, и имеют имя адаптера _вланкс_ , где X — это виртуальная ЛС, назначенная логической сети поставщика HNV (Transport).

Связь между двумя узлами Hyper-V, использующими логическую сеть поставщика HNV, может выполняться командой ping с дополнительным параметром секции (-c Y), где Y — это Секция сети TCPIP, в которой создаются Пахоствникс. Эту секцию можно определить, выполнив следующую команду:

```
C:\> ipconfig /allcompartments /all

<snip> ...
==============================================================================
Network Information for *Compartment 3*
==============================================================================
   Host Name . . . . . . . . . . . . : SA18n30-2
<snip> ...

Ethernet adapter VLAN11:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Microsoft Hyper-V Network Adapter
   Physical Address. . . . . . . . . : 40-1D-D8-B7-1C-04
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::5937:a365:d135:2899%39(Preferred)
   IPv4 Address. . . . . . . . . . . : 10.10.182.66(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.128
   Default Gateway . . . . . . . . . : 10.10.182.1
   NetBIOS over Tcpip. . . . . . . . : Disabled

Ethernet adapter VLAN11:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Microsoft Hyper-V Network Adapter
   Physical Address. . . . . . . . . : 40-1D-D8-B7-1C-05
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::28b3:1ab1:d9d9:19ec%44(Preferred)
   IPv4 Address. . . . . . . . . . . : 10.10.182.67(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.128
   Default Gateway . . . . . . . . . : 10.10.182.1
   NetBIOS over Tcpip. . . . . . . . : Disabled

*Ethernet adapter vEthernet (PAhostVNic):*
<snip> ...
```

>[!NOTE]
> Адаптеры узла PA vNIC не используются в пути к данным и поэтому не имеют IP-адреса, назначенного адаптеру "адаптера vethernet (Пахоствник)".

Например, предположим, что узлы Hyper-V 1 и 2 имеют IP-адреса HNV Provider (PA):

| Узел Hyper-V | IP-адрес PA 1 | IP-адрес PA 2 |
|--|--|--|
| Узел 1 | 10.10.182.64 | 10.10.182.65 |
| Узел 2 | 10.10.182.66 | 10.10.182.67 |

Мы можем проверить связь между двумя с помощью следующей команды для проверки подключения к логической сети поставщика HNV.

```
# Ping the first PA IP Address on Hyper-V Host 2 from the first PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.66 -S 10.10.182.64

# Ping the second PA IP Address on Hyper-V Host 2 from the first PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.67 -S 10.10.182.64

# Ping the first PA IP Address on Hyper-V Host 2 from the second PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.66 -S 10.10.182.65

# Ping the second PA IP Address on Hyper-V Host 2 from the second PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.67 -S 10.10.182.65
```

*Исправление* Если проверка связи с поставщиком HNV не работает, проверьте подключение к физической сети, включая конфигурацию виртуальной ЛС. Физические сетевые адаптеры на каждом узле Hyper-V должны находиться в режиме магистрали без определенной назначенной виртуальной ЛС. Узел управления vNIC должен быть изолирован к виртуальной ЛС логической сети управления.

```powershell
PS C:\> Get-NetAdapter "Ethernet 4" |fl

Name                       : Ethernet 4
InterfaceDescription       : <NIC> Ethernet Adapter
InterfaceIndex             : 2
MacAddress                 : F4-52-14-55-BC-21
MediaType                  : 802.3
PhysicalMediaType          : 802.3
InterfaceOperationalStatus : Up
AdminStatus                : Up
LinkSpeed(Gbps)            : 10
MediaConnectionState       : Connected
ConnectorPresent           : True
*VlanID                     : 0*
DriverInformation          : Driver Date 2016-08-28 Version 5.25.12665.0 NDIS 6.60

# VMM uses the older PowerShell cmdlet <Verb>-VMNetworkAdapterVlan to set VLAN isolation
PS C:\> Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName <Mgmt>

VMName VMNetworkAdapterName Mode     VlanList
------ -------------------- ----     --------
<snip> ...
       Mgmt                 Access   7
<snip> ...

# SDNExpress deployments use the newer PowerShell cmdlet <Verb>-VMNetworkAdapterIsolation to set VLAN isolation
PS C:\> Get-VMNetworkAdapterIsolation -ManagementOS

<snip> ...

IsolationMode        : Vlan
AllowUntaggedTraffic : False
DefaultIsolationID   : 7
MultiTenantStack     : Off
ParentAdapter        : VMInternalNetworkAdapter, Name = 'Mgmt'
IsTemplate           : True
CimSession           : CimSession: .
ComputerName         : SA18N30-2
IsDeleted            : False

<snip> ...
```

#### <a name="check-mtu-and-jumbo-frame-support-on-hnv-provider-logical-network"></a>Проверка поддержки кадров MTU и крупных размеров в логической сети поставщика HNV

Еще одна распространенная проблема в логической сети поставщика HNV заключается в том, что физические сетевые порты и/или плата Ethernet не имеют достаточного размера MTU, настроенного для снижения нагрузки на ВКСЛАН (или NVGRE).

>[!NOTE]
> Некоторые карты и драйверы Ethernet поддерживают новое ключевое слово * Енкаповерхеад, которое автоматически устанавливается агентом узла сетевого контроллера в значение 160. Затем это значение будет добавлено к значению ключевого слова * Жумбопаккет, сумма которого используется в качестве объявленного MTU.
> Например, * Енкаповерхеад = 160 и * Жумбопаккет = 1514 => MTU = 1674B

```
# Check whether or not your Ethernet card and driver support *EncapOverhead
PS C:\ > Test-EncapOverheadSettings

Verifying Physical Nic : <NIC> Ethernet Adapter #2
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Verifying Physical Nic : <NIC> Ethernet Adapter
Physical Nic  <NIC> Ethernet Adapter can support SDN traffic. Encapoverhead value set on the nic is  160
```

Чтобы проверить, поддерживает ли логическая сеть поставщика HNV более полный размер MTU, используйте командлет _Test-логикалнетворксуппортсжумбопаккет_ :

```powershell
# Get credentials for both source host and destination host (or use the same credential if in the same domain)
$sourcehostcred = Get-Credential
$desthostcred = Get-Credential

# Use the Management IP Address or FQDN of the Source and Destination Hyper-V hosts
Test-LogicalNetworkSupportsJumboPacket -SourceHost sa18n30-2 -DestinationHost sa18n30-3 -SourceHostCreds $sourcehostcred -DestinationHostCreds $desthostcred

# Failure Results
SourceCompartment : 3
pinging Source PA: 10.10.182.66 to Destination PA: 10.10.182.64 with Payload: 1632
pinging Source PA: 10.10.182.66 to Destination PA: 10.10.182.64 with Payload: 1472
Checking if physical nics support jumbo packets on host
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Cannot send jumbo packets to the destination. Physical switch ports may not be configured to support jumbo packets.
Checking if physical nics support jumbo packets on host
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Cannot send jumbo packets to the destination. Physical switch ports may not be configured to support jumbo packets.
```

*Исправление*
* Измените размер MTU на портах физического коммутатора как минимум 1674B (включая заголовок и трейлер Ethernet 14B).
* Если плата NIC не поддерживает ключевое слово Енкаповерхеад, измените ключевое слово Жумбопаккет, чтобы оно было как минимум 1674B

#### <a name="check-tenant-vm-nic-connectivity"></a>Проверка подключения сетевого адаптера виртуальной машины клиента
Каждая сетевая карта виртуальных машин, назначенная гостевой виртуальной машине, имеет сопоставление CA-PA между частным адресом клиента (CA) и пространством поставщика HNV (PA). Эти сопоставления хранятся в таблицах сервера ОВСДБ на каждом узле Hyper-V, и их можно найти, выполнив следующий командлет.

```
# Get all known PA-CA Mappings from this particular Hyper-V Host
PS > Get-PACAMapping

CA IP Address CA MAC Address    Virtual Subnet ID PA IP Address
------------- --------------    ----------------- -------------
10.254.254.2  00-1D-D8-B7-1C-43              4115 10.10.182.67
10.254.254.3  00-1D-D8-B7-1C-43              4115 10.10.182.67
192.168.1.5   00-1D-D8-B7-1C-07              4114 10.10.182.65
10.254.254.1  40-1D-D8-B7-1C-06              4115 10.10.182.66
192.168.1.1   40-1D-D8-B7-1C-06              4114 10.10.182.66
192.168.1.4   00-1D-D8-B7-1C-05              4114 10.10.182.66
```

>[!NOTE]
> Если для указанной виртуальной машины клиента не выводятся сопоставления CA-PA, проверьте ресурсы сетевого адаптера виртуальной машины и конфигурации IP-адресов на сетевом контроллере с помощью командлета _Get-нетворкконтроллернетворкинтерфаце_ . Кроме того, проверьте наличие установленных соединений между агентом узла NC и узлами сетевого контроллера.

Используя эти сведения, поставщик услуг размещения может инициировать проверку связи для виртуальной машины клиента с помощью командлета _Test-виртуалнетворкконнектион_ .

## <a name="specific-troubleshooting-scenarios"></a>Конкретные сценарии устранения неполадок

В следующих разделах приводятся рекомендации по устранению неполадок в конкретных сценариях.

### <a name="no-network-connectivity-between-two-tenant-virtual-machines"></a>Отсутствует сетевое подключение между двумя виртуальными машинами клиента

1.  Клиентом Убедитесь, что брандмауэр Windows на виртуальных машинах клиента не блокирует трафик.
2.  Клиентом Убедитесь, что IP-адреса назначены виртуальной машине клиента, выполнив _команду ipconfig_.
3.  Поставщика услуг размещения Выполните команду **Test-виртуалнетворкконнектион** с узла Hyper-V, чтобы проверить подключение между двумя виртуальными машинами клиента.

>[!NOTE]
>VSID ссылается на идентификатор виртуальной подсети. В случае с ВКСЛАН это идентификатор ВКСЛАН Network (вни). Это значение можно найти, выполнив командлет **Get-пакамаппинг** .

#### <a name="example"></a>Пример

```powershell
$password = ConvertTo-SecureString -String "password" -AsPlainText -Force
$cred = New-Object pscredential -ArgumentList (".\administrator", $password)
```

Создайте CA-ping между "зеленой веб-виртуальной машиной 1" и Сендерка IP-адресом 192.168.1.4 на узле "sa18n30-2.sa18.nttest.microsoft.com" с IP-адресом 10.127.132.153 на Листенерка IP-адрес 192.168.1.5, подключенных к виртуальной подсети (VSID) 4114.

```powershell
Test-VirtualNetworkConnection -OperationId 27 -HostName sa18n30-2.sa18.nttest.microsoft.com -MgmtIp 10.127.132.153 -Creds $cred -VMName "Green Web VM 1" -VMNetworkAdapterName "Green Web VM 1" -SenderCAIP 192.168.1.4 -SenderVSID 4114 -ListenerCAIP 192.168.1.5 -ListenerVSID 4114
Test-VirtualNetworkConnection at command pipeline position 1

Starting CA-space ping test
Starting trace session
Ping to 192.168.1.5 succeeded from address 192.168.1.4
Rtt = 0 ms

CA Routing Information:

    Local IP: 192.168.1.4
    Local VSID: 4114
    Remote IP: 192.168.1.5
    Remote VSID: 4114
    Distributed Router Local IP: 192.168.1.1
    Distributed Router Local MAC: 40-1D-D8-B7-1C-06
    Local CA MAC: 00-1D-D8-B7-1C-05
    Remote CA MAC: 00-1D-D8-B7-1C-07
    Next Hop CA MAC Address: 00-1D-D8-B7-1C-07

PA Routing Information:

    Local PA IP: 10.10.182.66
    Remote PA IP: 10.10.182.65

 <snip> ...
```

1. Клиентом Убедитесь, что на виртуальных подсетях или сетевых интерфейсах ВИРТУАЛЬНОЙ сети не указаны распределенные политики брандмауэра, которые блокируют трафик.

Запросите REST API сетевого контроллера, который находится в демонстрационной среде по адресу sa18n30nc в домене sa18.nttest.microsoft.com.

```
$uri = "https://sa18n30nc.sa18.nttest.microsoft.com"
Get-NetworkControllerAccessControlList -ConnectionUri $uri
```

## <a name="look-at-ip-configuration-and-virtual-subnets-which-are-referencing-this-acl"></a>Просмотреть IP-конфигурацию и виртуальные подсети, ссылающиеся на этот ACL

1. Поставщика услуг размещения Запустите ``Get-ProviderAddress`` на обоих узлах Hyper-v, где размещены две виртуальные машины клиента, а затем запустите ``Test-LogicalNetworkConnection`` или ``ping -c <compartment>`` с узла Hyper-v, чтобы проверить подключение в ЛОГИЧЕСКОЙ сети поставщика HNV.
2.  Поставщика услуг размещения Убедитесь, что на узлах Hyper-V установлены правильные параметры MTU и все устройства, переключающие между узлами Hyper-V. Запустите ``Test-EncapOverheadValue`` на всех узлах Hyper-V, которые находятся в вопросе. Кроме того, убедитесь, что для всех переключений уровня 2 между параметром MTU задано значение не менее 1674 байт, чтобы учитывать максимальную нагрузку на 160 байт.
3.  Поставщика услуг размещения Если IP-адреса PA отсутствуют и (или) подключение к центру сертификации разорвано, убедитесь, что политика сети получена. Выполните команду ``Get-PACAMapping`` , чтобы узнать, правильно ли установлены правила инкапсуляции и СОПОСТАВЛЕНИЯ CA-PA, необходимые для создания виртуальных сетей оверлея.
4.  Поставщика услуг размещения Убедитесь, что агент узла сетевого контроллера подключен к сетевому контроллеру. Выполните команду, ``netstat -anp tcp |findstr 6640`` чтобы проверить,
5.  Поставщика услуг размещения Убедитесь, что идентификатор узла в HKLM/соответствует ИДЕНТИФИКАТОРу экземпляра ресурсов сервера, на которых размещаются виртуальные машины клиента.
6. Поставщика услуг размещения Убедитесь, что идентификатор профиля порта соответствует ИДЕНТИФИКАТОРу экземпляра сетевых интерфейсов виртуальных машин клиента.

## <a name="logging-tracing-and-advanced-diagnostics"></a>Ведение журналов, трассировка и Расширенная диагностика

В следующих разделах приведены сведения о расширенной диагностике, ведении журнала и трассировке.

### <a name="network-controller-centralized-logging"></a>Централизованное ведение журналов сетевого контроллера

Сетевой контроллер может автоматически получать журналы отладчика и хранить их в централизованном расположении. Сбор журналов можно включить при первом развертывании сетевого контроллера или в любое другое время. Журналы собираются из сетевого контроллера, а сетевые элементы управляются сетевым контроллером: компьютерами размещения, подсистемами балансировки нагрузки программного обеспечения (SLB) и шлюзами.

Эти журналы содержат журналы отладки для кластера сетевого контроллера, приложения сетевого контроллера, журналов шлюзов, SLB, виртуальных сетей и распределенного брандмауэра. При добавлении нового узла, SLB или шлюза в сетевой контроллер на этих компьютерах запускается ведение журнала.
Аналогично, при удалении узла, SLB или шлюза из сетевого контроллера, ведение журнала на этих компьютерах останавливается.

#### <a name="enable-logging"></a>Включение ведения журналов

Ведение журнала включается автоматически при установке кластера сетевого контроллера с помощью командлета **Install-нетворкконтроллерклустер** . По умолчанию журналы собираются локально на узлах сетевого контроллера по адресу *%системдриве%\сдндиагностикс*. **Настоятельно рекомендуется** изменить это расположение на удаленную общую папку (не локальную).

Журналы кластера сетевого контроллера хранятся на сайте *%Програмдата%\виндовс фабрик\лог\трацес*. Можно указать централизованное расположение для сбора журналов с помощью параметра **диагностиклоглокатион** с рекомендацией, что это также удаленная общая папка.

Если вы хотите ограничить доступ к этому расположению, можно указать учетные данные доступа с помощью параметра **логлокатионкредентиал** . При предоставлении учетных данных для доступа к расположению журнала необходимо также указать параметр **кредентиаленкриптионцертификате** , который используется для шифрования учетных данных, хранимых локально на узлах сетевого контроллера.

При использовании параметров по умолчанию рекомендуется иметь не менее 75 ГБ свободного места в центральном расположении и 25 ГБ на локальных узлах (если не используется центральное расположение) для кластера сетевого контроллера с тремя узлами.

#### <a name="change-logging-settings"></a>Изменение параметров ведения журнала

Параметры ведения журнала можно изменить в любое время с помощью ``Set-NetworkControllerDiagnostic`` командлета. Можно изменить следующие параметры:

- **Расположение централизованного журнала**.  Можно изменить расположение для хранения всех журналов с помощью ``DiagnosticLogLocation`` параметра.
- **Учетные данные для доступа к расположению журнала**.  Вы можете изменить учетные данные для доступа к расположению журнала с ``LogLocationCredential`` параметром.
- **Переместить в локальное ведение журнала**.  Если вы указали централизованное расположение для хранения журналов, можно вернуться к локальному журналу на узлах сетевого контроллера с ``UseLocalLogLocation`` параметром (не рекомендуется из-за большого объема дискового пространства).
- **Область ведения журнала**.  По умолчанию собираются все журналы. Можно изменить область, чтобы она составила только журналы кластера сетевого контроллера.
- **Уровень ведения журнала**.  Уровень ведения журнала по умолчанию — информационный. Его можно изменить на Error, warning или verbose.
- **Время устаревания журнала**.  Журналы хранятся циклически. По умолчанию данные будут регистрироваться в течение 3 дней независимо от того, используется ли локальное ведение журнала или централизованное ведение журнала. Это ограничение времени можно изменить с помощью параметра **логтимелимитиндайс** .
- **Размер старения журнала**.  По умолчанию вы получите максимум 75 ГБ данных для ведения журнала при использовании централизованного ведения журнала и 25 ГБ при использовании локального ведения журнала. Это ограничение можно изменить с помощью параметра **логсизелимитинмбс** .

#### <a name="collecting-logs-and-traces"></a>Сбор журналов и трассировок

По умолчанию развертывания VMM используют централизованное ведение журналов для сетевого контроллера. Расположение общих файловых ресурсов для этих журналов указывается при развертывании шаблона службы сетевого контроллера.

Если расположение файла не указано, на каждом узле сетевого контроллера будет использоваться локальное ведение журнала с журналами, сохраненными в К:\виндовс\траЦинг\сдндиагностикс. Эти журналы сохраняются с помощью следующей иерархии:

- CrashDumps
- нкаппликатионкрашдумпс
- нкаппликатионлогс
- PerfCounters
- сдндиагностикс
- Трассировки

Сетевой контроллер использует Service Fabric (Azure). При устранении определенных проблем могут потребоваться Service Fabric журналы. Эти журналы можно найти на каждом узле сетевого контроллера в К:\програмдата\микрософт\сервице Fabric.

Если пользователь выполнил командлет _Debug-нетворкконтроллер_ , дополнительные журналы будут доступны на каждом узле Hyper-V, который был указан с помощью ресурса сервера в сетевом контроллере. Эти журналы (и трассировки, если они включены) хранятся в разделе К:\нкдиагностикс

### <a name="slb-diagnostics"></a>Диагностика SLB

#### <a name="slbm-fabric-errors-hosting-service-provider-actions"></a>Ошибки фабрики SLBM (действия поставщика услуг размещения)

1.  Убедитесь, что диспетчер программного обеспечения Load Balancer Manager (SLBM) работает и что уровни оркестрации могут взаимодействовать друг с другом: агентами SLB на основе SLBM-> и SLBM-> узлов SLB. Запустите [думпслбрестстате](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) из любого узла с доступом к КОНЕЧНОЙ точке RESTful сетевого контроллера.
2.  Проверьте *сднслбмперфкаунтерс* в PerfMon на одной из виртуальных машин узла сетевого контроллера (предпочтительный узел основного сетевого контроллера — Get-нетворкконтроллерреплика):
    1.  Подсистема обработки Load Balancer (фунтов) подключена к SLBM? (*Количество конфигураций SLBM лбенгине: Total* > 0)
    2.  По крайней мере знает о своих собственных конечных точках SLBM? (*Всего конечных точек виртуального IP-адреса* >= 2)
    3.  Подключены ли узлы Hyper-V (DIP) к SLBM? (*HP клиенты подключены* = = число серверов)
    4.  Подключен ли SLBM к мультиплексоров? (*Мультиплексоров подключено*  ==  *Мультиплексоров Исправен в SLBM*  ==  *Мультиплексоров Reporting "Исправен* " = # SLB мультиплексоров VMS.
3.  Убедитесь, что настроенный маршрутизатор BGP успешно пиринг с МУЛЬТИПЛЕКСОРом SLB
    1.  При использовании RRAS с удаленным доступом (т. е. виртуальной машины BGP):
        1.  Get-BgpPeer должен показывать подключение
        2.  Get-Бгпраутеинформатион должен отображать по крайней мере маршрут для самовиртуального IP-адреса SLBM.
    2.  Если используется физический коммутатор верхнего уровня (ToR) в качестве узла BGP, обратитесь к документации.
        1.  Например: # показывать экземпляр BGP
4.  Проверка счетчиков *слбмуксперфкаунтерс* и *SLBMUX* в PerfMon на ВИРТУАЛЬНОЙ машине мультиплексора SLB
5.  Проверка состояния конфигурации и диапазонов виртуальных IP-адресов в ресурсе программного Load Balancer Manager
    1.  Get-Нетворкконтроллерлоадбаланцерконфигуратион-ConnectionUri <https:// <FQDN or IP> | ConvertTo-JSON — глубина 8 (проверьте диапазоны виртуальных IP-адресов в пулах IP-адреса и убедитесь, что в пределах этих диапазонов используются виртуальные IP-адреса для Self-VIP (*лоадбаланацерманажерипаддресс*) и клиенты, имеющие доступ к клиентам)
        1. Get-Нетворкконтроллериппул-NetworkId "<общедоступный/частный виртуальный IP-адрес идентификатор ресурса логической сети>"-SubnetId "<общедоступный/частный VIP идентификатор ресурса логической подсети>"-ResourceId " <IP Pool Resource Id> "-ConnectionUri $URI | ConvertTo-JSON-Depth 8
    2.  Debug-Нетворкконтроллерконфигуратионстате-

Если какая-либо из перечисленных выше проверок завершается ошибкой, состояние SLB клиента также будет в режиме сбоя.

**Исправление** На основе приведенных ниже диагностических сведений исправьте следующее.
* Убедитесь, что мультиплексоры SLB подключены
  * Устранение проблем с сертификатами
  * Исправление сетевых неполадок
* Убедитесь, что сведения об пиринга BGP успешно настроены
* Убедитесь, что идентификатор узла в реестре совпадает с ИДЕНТИФИКАТОРом экземпляра сервера в ресурсе сервера (в справочном приложении для кода ошибки *хостнотконнектед* )
* Сбор журналов

#### <a name="slbm-tenant-errors-hosting-service-provider--and-tenant-actions"></a>Ошибки клиента SLBM (действия поставщика услуг хостинга и клиента)

1.  Поставщика услуг размещения Проверьте *отладку-нетворкконтроллерконфигуратионстате* , чтобы узнать, находятся ли какие-либо ресурсы подсистемы балансировки в состоянии ошибки. Попробуйте устранить проблемы, выполнив таблицу действий в приложении.
    1.  Проверка наличия конечной точки виртуального IP-адреса и объявлений
    2.  Проверьте количество обнаруженных конечных точек DIP для конечной точки виртуального IP-адреса.
2.  Клиентом Правильно указаны ресурсы Load Balancer проверки
    1.  Проверка конечных точек DIP, зарегистрированных в SLBM, на размещение виртуальных машин клиентов, соответствующих IP-конфигурациям пула адресов серверной части подсистемы балансировки нагрузки
3.  Поставщика услуг размещения Если DIP конечных точек не обнаруживаются или не подключены:
    1.  Проверьте *Debug-нетворкконтроллерконфигуратионстате*
        1.  Убедитесь, что агент NC и узел SLB успешно подключены к координатору событий сетевого контроллера с помощью``netstat -anp tcp |findstr 6640)``
    2.  Проверьте *HostID* в разделе реестра *nchostagent* Service RegKey (ссылка на код ошибки *Хостнотконнектед* в приложении) соответствует идентификатору экземпляра соответствующего ресурса сервера ( ``Get-NCServer |convertto-json -depth 8`` ).
    3.  Проверьте идентификатор профиля порта для порта виртуальной машины, соответствующий идентификатору экземпляра ресурса сетевого адаптера виртуальной машины
4.  [Поставщик услуг размещения] Получение журналов

#### <a name="slb-mux-tracing"></a>Трассировка мультиплексора SLB

Сведения из программного Load Balancer мультиплексоров также можно определить с помощью Просмотр событий.
1. В меню "вид Просмотр событий" щелкните "Показать журналы аналитики и отладки".
2. Перейдите к разделу "Журналы приложений и служб" > Microsoft > Windows > Слбмуксдривер > трассировка в Просмотр событий
3. Щелкните его правой кнопкой мыши и выберите пункт "включить журнал".

>[!NOTE]
>Рекомендуется включить это ведение журнала в течение короткого периода времени, пока вы пытаетесь воспроизвести проблему.

### <a name="vfp-and-vswitch-tracing"></a>Трассировка VFP и vSwitch

На любом узле Hyper-V, на котором размещена гостевая виртуальная машина, подключенная к виртуальной сети клиента, можно собрать трассировку VFP, чтобы определить, где могут находиться проблемы.

```
netsh trace start provider=Microsoft-Windows-Hyper-V-VfpExt overwrite=yes tracefile=vfp.etl report=disable provider=Microsoft-Windows-Hyper-V-VmSwitch
netsh trace stop
netsh trace convert .\vfp.etl ov=yes
```
