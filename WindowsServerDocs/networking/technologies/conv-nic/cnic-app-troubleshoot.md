---
title: Устранение неполадок конфигураций Объединенных сетевых адаптеров
description: Этот раздел является частью этого раздела в руководстве по настройке сетевого адаптера для Windows Server 2016.
ms.topic: article
ms.assetid: 0bc6746f-2adb-43d8-a503-52f473833164
manager: brianlic
ms.author: lizross
author: eross-msft
ms.date: 12/18/2020
ms.openlocfilehash: 524d73c759230b375d50cb6645e9c336684a18ea
ms.sourcegitcommit: 84b97d34d606b6bf4b6ec8760a93107f1b311428
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2021
ms.locfileid: "99245395"
---
# <a name="troubleshooting-converged-nic-configurations"></a>Устранение неполадок конфигураций Объединенных сетевых адаптеров

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Чтобы проверить, правильно ли настроена конфигурация RDMA на узле Hyper-V, можно использовать следующий сценарий.

- [Скачать скрипт Test-Rdma.ps1](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

Для устранения неполадок и проверки конфигурации Объединенных сетевых карт можно также использовать следующие команды Windows PowerShell.

## <a name="get-netadapterrdma"></a>Get-NetAdapterRdma

Чтобы проверить конфигурацию RDMA сетевого адаптера, выполните следующую команду Windows PowerShell на сервере Hyper-V.

```powershell
Get-NetAdapterRdma | fl *
```

Чтобы определить и устранить проблемы после выполнения этой команды на узле Hyper-V, можно использовать следующие ожидаемые и непредвиденные результаты.

### <a name="get-netadapterrdma-expected-results"></a>Ожидаемые результаты Get-NetAdapterRdma

Узел vNIC и физический сетевой адаптер отображают ненулевые возможности RDMA.

![Ожидаемые результаты Windows PowerShell](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-01.jpg)

### <a name="get-netadapterrdma-unexpected-results"></a>Get-NetAdapterRdma непредвиденные результаты

Если при выполнении команды **Get-нетадаптеррдма** получены непредвиденные результаты, выполните следующие действия.

1. Убедитесь, что драйверы минипорта Млнкс и шины Млнкс установлены последними. Для Mellanox используйте как минимум Drop 42.
2. Проверьте, соответствуют ли драйверы минипорта и шины Млнкс, путем проверки версии драйвера с помощью диспетчер устройств. Драйвер шины можно найти в системном устройстве. Имя должно начинаться с Mellanox Connect-X 3 PRO VPI, как показано на следующем снимке экрана свойств сетевого адаптера.

   ![Снимок экрана: вкладка сведений диалогового окна "Свойства" Mellanox ConnectX-3 Pro Есернетадаптер и вкладка "драйвер" в диалоговом окне "Свойства сетевого адаптера Mellanox ConnectX-3 Pro".](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-02.jpg)

4. Убедитесь, что сеть Direct (RDMA) включена как на физическом сетевом адаптере, так и на узле vNIC.
5. Убедитесь, что vSwitch создан на правильном физическом адаптере, проверив его возможности RDMA.
6. Проверьте системный журнал Евентвиевер и выполните фильтрацию по исходному параметру Hyper-V-VmSwitch.

## <a name="get-smbclientnetworkinterface-verifies-rdma-configuration"></a>Get-SmbClientNetworkInterface проверяет конфигурацию RDMA

В качестве дополнительного шага для проверки конфигурации RDMA выполните следующую команду Windows PowerShell на сервере Hyper-V.

```powershell
Get-SmbClientNetworkInterface
```

### <a name="get-smbclientnetworkinterface-expected-results"></a>Ожидаемые результаты Get-SmbClientNetworkInterface

Узел vNIC должен выглядеть так же, как RDMA, с точки зрения SMB.

![Снимок экрана окна PowerShell, отображающего результат выполнения командлета Get-SmbClientNetworkInterface.](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-03.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Get-SmbClientNetworkInterface непредвиденные результаты

1. Убедитесь, что драйверы минипорта Млнкс и шины Млнкс установлены последними. Для Mellanox используйте как минимум Drop 42.
2. Проверьте, соответствуют ли драйверы минипорта и шины Млнкс, путем проверки версии драйвера с помощью диспетчер устройств. Драйвер шины можно найти в системном устройстве. Имя должно начинаться с Mellanox Connect-X 3 PRO VPI, как показано на следующем снимке экрана свойств сетевого адаптера.
3. Убедитесь, что сеть Direct (RDMA) включена как на физическом сетевом адаптере, так и на узле vNIC.
4. Убедитесь, что виртуальный коммутатор Hyper-V создан на правильном физическом адаптере, проверив его возможности RDMA.
5. Проверьте журналы Евентвиевер для "клиента SMB" в **приложении и службах | Microsoft | Windows**.

## <a name="get-netadapterqos"></a>Get-NetAdapterQos

Чтобы просмотреть конфигурацию качества обслуживания сетевого адаптера \( \) , выполнив следующую команду Windows PowerShell.

```powershell
Get-NetAdapterQos
```

### <a name="get-netadapterqos-expected-results"></a>Ожидаемые результаты Get-NetAdapterQos

Приоритеты и классы трафика должны отображаться в соответствии с первым этапом настройки, выполненным с помощью этого руководством.

![Приоритеты и классы качества обслуживания](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-04.jpg)

### <a name="get-netadapterqos-unexpected-results"></a>Get-NetAdapterQos непредвиденные результаты

Если результаты являются непредвиденными, выполните следующие действия.

1. Убедитесь, что физический сетевой адаптер поддерживает мосты "центр обработки данных" \( \) и "качество обслуживания"
2. Убедитесь, что драйверы сетевых адаптеров обновлены.

## <a name="get-smbmultichannelconnection"></a>Get-SmbMultiChannelConnection

Чтобы убедиться, что IP-адрес удаленного узла поддерживает RDMA, можно использовать следующую команду Windows PowerShell \- .

```powershell
Get-SmbMultiChannelConnection
```

### <a name="get-smbmultichannelconnection-expected-results"></a>Ожидаемые результаты Get-SmbMultiChannelConnection

IP-адрес удаленного узла отображается как поддерживающий RDMA.

![IP-адрес удаленного узла с поддержкой RDMA](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-05.jpg)

### <a name="get-smbmultichannelconnection-unexpected-results"></a>Get-SmbMultiChannelConnection непредвиденные результаты

Если результаты являются непредвиденными, выполните следующие действия.

1. Убедитесь, что проверка связи выполняется обоими способами.
2. Убедитесь, что брандмауэр не блокирует инициацию подключения по протоколу SMB. В частности, включите правило брандмауэра для порта Direct SMB 5445 для iWARP и 445 для РОЦЕ.

## <a name="get-smbclientnetworkinterface-verifies-nic-is-rmda-capable"></a>Get-SmbClientNetworkInterface проверяет, поддерживает ли сетевой адаптер РМДА

Можно использовать следующую команду, чтобы убедиться, что виртуальный сетевой адаптер, включенный для RDMA, сообщается в виде RDMA \- с поддержкой протокола SMB.

```powershell
Get-SmbClientNetworkInterface
```

### <a name="get-smbclientnetworkinterface-expected-results"></a>Ожидаемые результаты Get-SmbClientNetworkInterface

Виртуальный сетевой адаптер, для которого включен параметр RDMA, должен рассматриваться как RDMA, поддерживающий протокол SMB.

![Сообщения SMB, поддерживающие адаптеры RDMA](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-06.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Get-SmbClientNetworkInterface непредвиденные результаты

Если результаты являются непредвиденными, выполните следующие действия.

1. Убедитесь, что проверка связи выполняется обоими способами.
2. Убедитесь, что брандмауэр не блокирует инициацию подключения по протоколу SMB.

## <a name="vstat-mellanox-specific"></a>\(Специальная Mellanox для VSTA\)

При использовании сетевых адаптеров Mellanox можно использовать команду **VSTA** для проверки RDMA на \( \) узлах Hyper-V с согласованной версией Ethernet роце.

### <a name="vstat-expected-results"></a>Ожидаемые результаты для VSTA

Версия Роце на обоих узлах должна быть одинаковой. Это также хороший способ проверить, является ли версия встроенного по на обоих узлах последней.

![Примеры результатов проверки версии Роце](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-07.jpg)

### <a name="vstat-unexpected-results"></a>непредвиденные результаты VSTA

Если результаты являются непредвиденными, выполните следующие действия.

1. Задать правильную версию Роце с помощью Set-MlnxDriverCoreSetting
2. Установите последнюю версию встроенного по с веб-сайта Mellanox.

## <a name="perfmon-counters"></a>Счетчики системного монитора

Вы можете просмотреть счетчики в системном мониторе, чтобы проверить активность RDMA вашей конфигурации.

![Примеры результатов системного монитора](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-08.jpg)

## <a name="related-topics"></a>Связанные темы

- [Конфигурация с согласованным СЕТЕВЫМ адаптером с одним сетевым адаптером](cnic-single.md)
- [Конфигурация сетевого адаптера Объединенных сетевых адаптеров](cnic-datacenter.md)
- [Конфигурация физического коммутатора для Объединенных сетевых адаптеров](cnic-app-switch-config.md)
