---
title: Дополнительные свойства NIC
description: Управлять сетевыми картами и всеми функциями можно с помощью Windows PowerShell или панели управления сетью.
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/20/2018
ms.openlocfilehash: aa26e3ef83ec6255da6a386ecfce34a7501ae3f5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955641"
---
# <a name="nic-advanced-properties"></a>Дополнительные свойства NIC

Управлять сетевыми картами и всеми функциями можно через Windows PowerShell с помощью командлета [NetAdapter](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps&viewFallbackFrom=winserverr2-ps) .  Также можно управлять сетевыми картами и всеми функциями с помощью панели управления сетью (ncpa.cpl).

1. В **Windows PowerShell**выполните `Get‑NetAdapterAdvancedProperties` командлет для двух различных способов создания или модели сетевых карт.

   ![Get-Нетадаптерадванцедпроперти M1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-m1.png)

   ![Get-Нетадаптерадванцедпроперти C1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-c1.png)

   В этих двух списках дополнительных свойств сетевого адаптера есть сходства и различия.

2. На **панели управления сетью** (ncpa.cpl) выполните следующие действия.

   а. Щелкните сетевую карту правой кнопкой мыши.

   ![Диалоговое окно "Сетевые подключения"](../../media/network-offload-and-optimization/network-connections-dialog.png)

   b. В диалоговом окне Свойства нажмите кнопку **настроить**.

    ![Свойства C1](../../media/network-offload-and-optimization/c1-properties.png)

   c. Перейдите на вкладку **Дополнительно** , чтобы просмотреть дополнительные свойства.<p>Элементы в этом списке сопоставляются с элементами в `Get-NetAdapterAdvancedProperties` выходных данных.

   ![Свойства сетевого адаптера Chelsio](../../media/network-offload-and-optimization/chelsio-network-adapter-properties.png)

---
