---
title: Команды Windows PowerShell для RSS и vRSS
description: В этом разделе вы узнаете, как быстро находить технические справочные сведения о командах Windows PowerShell для масштабирования на стороне приема (RSS) и виртуальных RSS (vRSS).
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 49e93b9f-46d9-4cee-bcda-1c4634893ddd
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/05/2018
ms.openlocfilehash: bb915f72e53d28c73a9c2e405b3b0edd656953db
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405276"
---
# <a name="windows-powershell-commands-for-rss-and-vrss"></a>Команды Windows PowerShell для RSS и vRSS

>Относится к: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе вы узнаете, как быстро находить технические справочные сведения о командах Windows PowerShell для масштабирования на стороне приема \(RSS @ no__t-1 и Virtual RSS \(vRSS @ no__t-3.

Используйте следующие команды RSS для настройки RSS на физическом компьютере с несколькими процессорами или несколькими ядрами. Вы можете использовать те же команды для настройки vRSS на виртуальной машине \(VM @ no__t-1, работающей под управлением поддерживаемой операционной системы. Дополнительные сведения см. [в разделе командлеты сетевого адаптера в Windows PowerShell](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps).

## <a name="configure-vmq"></a>Настройка VMQ

для vRSS требуется, чтобы VMQ была включена и настроена. Для управления параметрами VMQ можно использовать следующие команды Windows PowerShell.

- [Disable-Нетадаптервмк](https://docs.microsoft.com/powershell/module/netadapter/disable-netadaptervmq?view=win10-ps)
- [Enable-Нетадаптервмк](https://docs.microsoft.com/powershell/module/netadapter/enable-netadaptervmq?view=win10-ps)
- [Get-Нетадаптервмк](https://docs.microsoft.com/powershell/module/netadapter/get-netadaptervmq?view=win10-ps)
- [Set-Нетадаптервмк](https://docs.microsoft.com/powershell/module/netadapter/set-netadaptervmq?view=win10-ps)

## <a name="enable-and-configure-rss-on-a-native-host"></a>Включение и Настройка RSS на собственном узле

Используйте следующие команды PowerShell, чтобы настроить RSS на собственном узле, а также управлять RSS в виртуальной машине или виртуальным сетевым адаптером узла (vNIC). Некоторые параметры этих команд также могут влиять на очередь виртуальной машины \(VMQ @ no__t-1 на узле Hyper-V.  

>[!IMPORTANT]
>Включение RSS в виртуальной машине или узле vNIC является необходимым условием для включения и использования vRSS.

- [Disable-Нетадаптеррсс](https://docs.microsoft.com/powershell/module/netadapter/disable-netadapterrss?view=win10-ps)
- [Enable-Нетадаптеррсс](https://docs.microsoft.com/powershell/module/netadapter/enable-netadapterrss?view=win10-ps)
- [Get-Нетадаптеррсс](https://docs.microsoft.com/powershell/module/netadapter/get-netadapterrss?view=win10-ps)
- [Set-Нетадаптеррсс](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss?view=win10-ps)

## <a name="enable-vrss-on-the-hyper-v-virtual-switch-port"></a>Включение vRSS на порт виртуального коммутатора Hyper @ no__t-0V

Помимо включения RSS в виртуальной машине vRSS требует включения vRSS на порт виртуального коммутатора Hyper @ no__t-0V. 

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
>Относится к: Windows Server 2019

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
>Относится к: Windows Server 2019

Чтобы определить текущий режим планирования или изменить режим планирования для узла vNIC, используйте следующие команды Windows PowerShell:

   **Просмотр текущих параметров:** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **Установка или изменение режима планирования:** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## <a name="related-topics"></a>См. также 
Дополнительные сведения см. в следующих справочных разделах.

- [Get-VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmnetworkadapter)
- [Set-VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmnetworkadapter)

Дополнительные сведения см. в статье [виртуальное масштабирование на стороне приема (vRSS)](vrss-top.md).