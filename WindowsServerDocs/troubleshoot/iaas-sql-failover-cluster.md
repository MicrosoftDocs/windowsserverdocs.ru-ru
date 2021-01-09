---
title: Настройка базовых показателей порогового значения сети отказоустойчивого кластера
description: В этой статье описаны решения для настройки пороговых значений сетей отказоустойчивого кластера.
ms.date: 05/28/2020
author: Deland-Han
ms.author: delhan
ms.topic: troubleshooting
ms.openlocfilehash: 5cce39ea42af57bbfd400427f763dfca5da75d7b
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2021
ms.locfileid: "98040304"
---
# <a name="iaas-with-sql-server---tuning-failover-cluster-network-thresholds"></a>IaaS с настройками пороговых значений сети отказоустойчивого кластера SQL Server

В этой статье описаны решения для настройки пороговых значений сетей отказоустойчивого кластера.

## <a name="symptom"></a>Симптом

При запуске узлов отказоустойчивого кластера Windows в IaaS с группой доступности SQL Server Always On рекомендуется изменить параметр кластера на более неявное состояние мониторинга. Параметры кластера не включены в список ограничений и могут привести к ненужным простоям. Параметры по умолчанию предназначены для высокой настройки в локальных сетях и не предусматривают возможность принудительной задержки, вызванной многоклиентской средой, такой как Windows Azure (IaaS).

Отказоустойчивая кластеризация Windows Server постоянно отслеживает сетевые подключения и работоспособность узлов в кластере Windows.  Если узел недоступен по сети, выполняется восстановление, чтобы приложения и службы стали снова доступны в сети на другом узле кластера. Задержка связи между узлами кластера может привести к следующей ошибке:

> Ошибка 1135 (системный журнал событий)

Узел кластера **NODE1** был удален из активного членства отказоустойчивого кластера. Возможно, служба кластеров на этом узле остановлена. Это также может быть вызвано тем, что узел потерял связь с другими активными узлами в отказоустойчивом кластере. Запустите мастер проверки конфигурации, чтобы проверить конфигурацию сети. Если условие сохраняется, проверьте наличие ошибок оборудования или программного обеспечения, связанных с сетевыми адаптерами на этом узле. Также проверьте наличие сбоев в любых других сетевых компонентах, к которым подключен узел, например к концентраторам, коммутаторам или мостам.

Пример Cluster. log:

```console
0000ab34.00004e64::2014/06/10-07:54:34.099 DBG   [NETFTAPI] Signaled NetftRemoteUnreachable event, local address 10.xx.x.xxx:3343 remote address 10.x.xx.xx:3343
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] got event: Remote endpoint 10.xx.xx.xxx:~3343~ unreachable from 10.xx.x.xx:~3343~
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Marking Route from 10.xxx.xxx.xxxx:~3343~ to 10.xxx.xx.xxxx:~3343~ as down
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [NDP] Checking to see if all routes for route (virtual) local fexx::xxx:5dxx:xxxx:3xxx:~0~ to remote xxx::cxxx:xxxd:xxx:dxxx:~0~ are down
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [NDP] All routes for route (virtual) local fxxx::xxxx:5xxx:xxxx:3xxx:~0~ to remote fexx::xxxx:xxxx:xxxx:xxxx:~0~ are down
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [CORE] Node 8: executing node 12 failed handlers on a dedicated thread
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: Cleaning up connections for n12.
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [Nodename] Clearing 0 unsent and 15 unacknowledged messages.
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: n12 node object is closing its connections
0000ab34.00008b68::2014/06/10-07:54:34.099 INFO  [DCM] HandleNetftRemoteRouteChange
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 1: Old: 05.936, Message: Response, Route sequence: 150415, Received sequence: 150415, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:28.000, Ticks since last sending: 4
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: closing n12 node object channels
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 2: Old: 06.434, Message: Request, Route sequence: 150414, Received sequence: 150402, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:27.665, Ticks since last sending: 36
0000ab34.0000a8ac::2014/06/10-07:54:34.099 INFO  [DCM] HandleRequest: dcm/netftRouteChange
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 3: Old: 06.934, Message: Response, Route sequence: 150414, Received sequence: 150414, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:27.165, Ticks since last sending: 4
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 4: Old: 07.434, Message: Request, Route sequence: 150413, Received sequence: 150401, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:26.664, Ticks since last sending: 36
```

```console
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <realLocal>10.xxx.xx.xxx:~3343~</realLocal>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <realRemote>10.xxx.xx.xxx:~3343~</realRemote>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <virtualLocal>fexx::xxxx:xxxx:xxxx:xxxx:~0~</virtualLocal>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <virtualRemote>fexx::xxxx:xxxx:xxxx:xxxx:~0~</virtualRemote>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Delay>1000</Delay>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Threshold>5</Threshold>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Priority>140481</Priority>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Attributes>2147483649</Attributes>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO  </struct mscs::FaultTolerantRoute>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO   removed
```

```console
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   [QUORUM] Node 8: Lost quorum (3 4 5 6 7 8)
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   [QUORUM] Node 8: goingAway: 0, core.IsServiceShutdown: 0
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   lost quorum (status = 5925)
```

## <a name="cause"></a>Причина

Существует два параметра, которые используются для настройки работоспособности подключения кластера.

**Delay** — определяет частоту, с которой пульсы кластера передаются между узлами.  Задержка — это количество секунд до отправки следующего пульса.  В одном кластере могут существовать разные задержки между узлами в одной подсети и между узлами, которые находятся в разных подсетях.

**Threshold (порог** ) — определяет число пульсов, пропущенных до того, как кластер примет действие по восстановлению.  Пороговое значение — число пульсов.  В одном кластере могут существовать разные пороговые значения между узлами в одной подсети и между узлами, находящихся в разных подсетях.

По умолчанию Windows Server 2016 устанавливает для **самесубнетсрешолд** значение 10, а для **самесубнетделай** — 1000 мс. Например, если наблюдение за подключением не выполняется в течение 10 секунд, пороговое значение отработки отказа достигается в результате недоступности узла, удаляемого из членства в кластере. В результате ресурсы перемещаются на другой доступный узел в кластере. Сообщается об ошибках кластера, включая ошибки кластера 1135 (см. выше).

## <a name="resolution"></a>Решение

В среде IaaS параметры конфигурации сети кластера ослабляется.

### <a name="steps-to-verify-current-configuration"></a>Действия для проверки текущей конфигурации

Проверьте текущие параметры конфигурации сети кластера, используя команду Get-cluster:

```powershell
C:\Windows\system32> get-cluster | fl *subnet*
```

По умолчанию, минимальное, максимальное и рекомендованное значение для каждой ОС поддержки

| Описание | ОС | Min | Max | По умолчанию | Рекомендуемая |
|--|--|--|--|--|--|
| CrossSubnetThreshold | 2008 R2 | 3 | 20 | 5 | 20 |
| Пороговое значение Кросссубнет | 2012 | 3 | 120 | 5 | 20 |
| Пороговое значение Кросссубнет | 2012 R2 | 3 | 120 | 5 | 20 |
| Пороговое значение Кросссубнет | 2016 | 3 | 120 | 20 | 20 |
| Пороговое значение Самесубнет | 2008 R2 | 3 | 10 | 5 | 10 |
| Пороговое значение Самесубнет | 2012 | 3 | 120 | 5 | 10 |
| Пороговое значение Самесубнет | 2012 R2 | 3 | 120 | 5 | 10 |
| SameSubnetThreshold | 2016 | 3 | 120 | 10 | 10 |

Значения порога соответствуют текущим рекомендациям относительно области развертывания, как описано в следующей статье:

[Тонкая настройка пороговых значений сети отказоустойчивого кластера в Windows Server 2012 R2](https://support.microsoft.com/en-us/help/3153887/fine-tuning-failover-cluster-network-thresholds-in-windows-server-2012)

**Пороговое значение** определяет количество периодических сигналов, пропущенных до того, как кластер примет действие по восстановлению.  Пороговое значение — число пульсов.  В одном кластере могут существовать разные пороговые значения между узлами в одной подсети и между узлами, которые находятся в разных подсетях.

## <a name="recommendations-for-changing-to-more-relaxed-settings-for-multi-tenant-environments-like-azure-iaas"></a>Рекомендации по переходу к более строгим параметрам для сред с несколькими клиентами, таких как Azure (IaaS)

> [!NOTE]
> Увеличение устойчивости к кластерной среде путем настройки параметров конфигурации сети кластера может привести к увеличению времени простоя. Дополнительные сведения см. в разделе [Настройка пороговых значений сети для отказоустойчивого кластера](https://techcommunity.microsoft.com/t5/failover-clustering/tuning-failover-cluster-network-thresholds/ba-p/371834).

1. Измените параметры на более строгие:

    > [!NOTE]
    > Изменение порогового значения кластера вступит в силу немедленно, вам не придется перезапускать кластер или ресурсы.

    Следующие параметры рекомендуются для обеих подсетей и развертываний групп доступности в разных регионах.

    ```powershell
    C:\Windows\system32> (get-cluster).SameSubnetThreshold = 20
    ```

    ```powershell
    C:\Windows\system32> (get-cluster).CrossSubnetThreshold = 20
    ```

2. Проверьте изменения:

    ```powershell
    C:\Windows\system32> get-cluster | fl *subnet*
    ```

    :::image type="content" source="media/iaas-sql-failover-cluster/cmd.png" alt-text="cmd" border="false":::

## <a name="references"></a>Ссылки

Дополнительные сведения о настройке параметров сетевой конфигурации кластера Windows см. в разделе [Настройка пороговых значений сети для отказоустойчивого кластера](https://techcommunity.microsoft.com/t5/failover-clustering/tuning-failover-cluster-network-thresholds/ba-p/371834).

Сведения об использовании cluster.exe для настройки параметров конфигурации сети кластера Windows см. [в статье Настройка сетей кластера для отказоустойчивого кластера](/previous-versions/office/exchange-server-2007/bb690953(v=exchg.80)?redirectedfrom=MSDN).
