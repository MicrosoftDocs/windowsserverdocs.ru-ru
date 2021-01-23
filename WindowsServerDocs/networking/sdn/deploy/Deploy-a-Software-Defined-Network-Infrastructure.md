---
title: Развертывание инфраструктуры программно-конфигурируемой сети
description: Этот раздел содержит ссылки на разделы, посвященные развертыванию инфраструктуры программно-определяемой сети (SDN) с помощью сценариев в Windows Server 2019 и 2016.
ms.topic: how-to
ms.assetid: 6c665c88-df28-4150-81d4-a47e9fa5255c
ms.date: 08/23/2018
ms.author: anpaul
author: AnirbanPaul
manager: grcusanz
ms.openlocfilehash: a9ce251488d80b4e5180d1641bc2157227d08d71
ms.sourcegitcommit: fb2ae5e6040cbe6dde3a87aee4a78b08f9a9ea7c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2021
ms.locfileid: "98716020"
---
# <a name="deploy-a-software-defined-network-infrastructure"></a>Развертывание программно-определяемой сетевой инфраструктуры

>Применяется к: Windows Server 2019, Windows Server 2016

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