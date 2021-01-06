---
title: Развертывание инфраструктуры программно-конфигурируемой сети
description: Этот раздел содержит ссылки на разделы, посвященные развертыванию инфраструктуры программно-определяемой сети (SDN) с помощью сценариев в Windows Server 2016.
ms.topic: how-to
ms.assetid: 6c665c88-df28-4150-81d4-a47e9fa5255c
ms.date: 08/23/2018
ms.author: anpaul
author: AnirbanPaul
manager: grcusanz
ms.openlocfilehash: 43bb1af29735dd1bf8ba911690abb78a09f1cf0d
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950120"
---
# <a name="deploy-a-software-defined-network-infrastructure"></a>Развертывание программно-определяемой сетевой инфраструктуры

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Развертывание инфраструктуры программно-определяемой сети (SDN) корпорации Майкрософт.

Эти развертывания включают все необходимые технологии для полностью функциональной инфраструктуры, включая виртуализацию сети Hyper-V (HNV), сетевые контроллеры, подсистемы балансировки нагрузки программного обеспечения (SLB и МУЛЬТИПЛЕКСОР) и шлюзы.

## <a name="set-up-sdn-infrastructure-in-the-vmm-fabric"></a>Настройка инфраструктуры SDN в структуре VMM




-   [Настройка инфраструктуры программно-определяемой сети (SDN) в структуре VMM](/system-center/vmm/deploy-sdn)

    Используйте этот метод, если вы хотите включить диспетчер виртуальных машин System Center (VMM) для управления инфраструктурой SDN.

## <a name="deploy-sdn-infrastructure-using-scripts"></a>Развертывание инфраструктуры SDN с помощью сценариев

-   [Развертывание инфраструктуры программно-конфигурируемой сети с помощью скриптов](../../sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)

    Используйте этот метод, если вы не хотите использовать VMM для управления инфраструктурой SDN или если у вас есть другой метод управления.


## <a name="deploy-individual-sdn-technologies-instead-of-an-entire-infrastructure"></a>Развертывание отдельных технологий SDN вместо всей инфраструктуры
 Если вы хотите развернуть отдельные технологии SDN вместо всей инфраструктуры, см. раздел [развертывание программно определенных сетевых технологий с помощью Windows PowerShell](Deploy-Software-Defined-Network-Technologies-using-Windows-PowerShell.md).








## <a name="related-topics"></a>Связанные темы
- [Программно-конфигурируемая сеть (SDN)](../software-defined-networking.md)
- [Технологии SDN](../technologies/Software-Defined-Networking-Technologies.md)
- [Планирование SDN](../plan/plan-a-software-defined-network-infrastructure.md)
- [Управление SDN](../manage/manage-sdn.md)
- [Безопасность в SDN](../security/sdn-security-top.md)
- [Устранение неполадок SDN](../troubleshoot/Troubleshoot-Software-Defined-Networking.md)