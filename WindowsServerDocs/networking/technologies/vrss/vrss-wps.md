---
title: Команды Windows PowerShell для RSS и vRSS
description: В этом разделе вы узнаете, как быстро находить технические справочные сведения о командах Windows PowerShell для масштабирования на стороне приема (RSS) и виртуальных RSS (vRSS).
ms.topic: article
ms.assetid: 49e93b9f-46d9-4cee-bcda-1c4634893ddd
ms.localizationpriority: medium
manager: dougkim
ms.author: jgerend
author: JasonGerend
ms.date: 09/05/2018
ms.openlocfilehash: 4a31b52909aa009f40201d97a40419f13f1fb525
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101829203"
---
# <a name="windows-powershell-commands-for-rss-and-vrss"></a>Команды Windows PowerShell для RSS и vRSS

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе вы узнаете, как быстро находить технические справочные сведения о командах Windows PowerShell для масштабирования на стороне приема \( RSS \) и виртуального RSS-канала \( \) .

Используйте следующие команды RSS для настройки RSS на физическом компьютере с несколькими процессорами или несколькими ядрами. Вы можете использовать те же команды для настройки vRSS на виртуальной машине виртуальной \( машины \) , работающей под управлением поддерживаемой операционной системы. Дополнительные сведения см. [в разделе командлеты сетевого адаптера в Windows PowerShell](/powershell/module/netadapter/).

## <a name="configure-vmq"></a>Настройка VMQ

для vRSS требуется, чтобы VMQ была включена и настроена. Для управления параметрами VMQ можно использовать следующие команды Windows PowerShell.

- [Disable-Нетадаптервмк](/powershell/module/netadapter/disable-netadaptervmq)
- [Enable-Нетадаптервмк](/powershell/module/netadapter/enable-netadaptervmq)
- [Get-Нетадаптервмк](/powershell/module/netadapter/get-netadaptervmq)
- [Set-Нетадаптервмк](/powershell/module/netadapter/set-netadaptervmq)

## <a name="enable-and-configure-rss-on-a-native-host"></a>Включение и Настройка RSS на собственном узле

Используйте следующие команды PowerShell, чтобы настроить RSS на собственном узле, а также управлять RSS в виртуальной машине или виртуальным сетевым адаптером узла (vNIC). Некоторые параметры этих команд также могут повлиять на очередь виртуальной машины \( VMQ \) на узле Hyper-V.

>[!IMPORTANT]
>Включение RSS в виртуальной машине или узле vNIC является необходимым условием для включения и использования vRSS.

- [Disable-Нетадаптеррсс](/powershell/module/netadapter/disable-netadapterrss)
- [Enable-Нетадаптеррсс](/powershell/module/netadapter/enable-netadapterrss)
- [Get-Нетадаптеррсс](/powershell/module/netadapter/get-netadapterrss)
- [Set-Нетадаптеррсс](/powershell/module/netadapter/Set-NetAdapterRss)

## <a name="enable-vrss-on-the-hyper-v-virtual-switch-port"></a>Включение vRSS на \- порте виртуального коммутатора Hyper V

Помимо включения RSS в виртуальной машине, для vRSS необходимо включить vRSS на \- порте виртуального коммутатора Hyper-V.

Определите существующие параметры vRSS и включите или отключите функцию для виртуальной машины.

   **Просмотр текущих параметров:**

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **Включена функция:**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## <a name="enable-or-disable-vrss-on-a-host-vnic"></a>Включение и отключение vRSS на узле vNIC

Определите существующие параметры vRSS и включите или отключите функцию для узла vNIC.

   **Просмотр текущих параметров:**

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **Включить или отключить функцию:**

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## <a name="configure-the-scheduling-mode-on-the-hyper-v-virtual-switch-port"></a>Настройка режима планирования для порта виртуального коммутатора Hyper-V
>Область применения: Windows Server 2019

В Windows Server 2019 vRSS может обновлять логические процессоры, используемые для динамической обработки сетевого трафика.  Устройства с поддерживаемыми драйверами по умолчанию включены в этот режим планирования.

Определение текущего режима планирования в системе или изменение режима планирования для виртуальной машины.

   **Просмотр текущих параметров:**

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **Установка или изменение режима планирования:**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## <a name="configure-the-scheduling-mode-on-a-host-vnic"></a>Настройка режима планирования на узле vNIC
>Область применения: Windows Server 2019

Чтобы определить текущий режим планирования или изменить режим планирования для узла vNIC, используйте следующие команды Windows PowerShell:

   **Просмотр текущих параметров:**

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **Установка или изменение режима планирования:**

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## <a name="related-topics"></a>Связанные разделы
Дополнительные сведения см. в следующих справочных разделах.

- [Get-VMNetworkAdapter](/powershell/module/hyper-v/get-vmnetworkadapter)
- [Set-VMNetworkAdapter](/powershell/module/hyper-v/set-vmnetworkadapter)

Дополнительные сведения см. в статье [виртуальное масштабирование на стороне приема (vRSS)](vrss-top.md).
