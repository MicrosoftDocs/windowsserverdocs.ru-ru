---
title: Развертывание службы защиты узла
ms.topic: article
ms.assetid: 310b63d9-5ac7-4961-98ef-103af45d706a
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 01/14/2020
ms.openlocfilehash: e8077655717db3f6700b0e0a3d12792465b41299
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939775"
---
# <a name="deploying-the-host-guardian-service"></a>Развертывание службы защиты узла

>Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016

Одной из наиболее важных целей предоставления размещенной среды является обеспечение безопасности виртуальных машин, работающих в среде. Поставщики облачных служб и администраторы корпоративного частного облака могут использовать защищенную структуру для создания более безопасной среды для виртуальных машин. Защищенная структура состоит из одной службы защиты узла (HGS), которая обычно представлена кластером из трех узлов, одним или несколькими защищенными узлами и набором экранированных виртуальных машин.

## <a name="video-deploying-a-guarded-fabric"></a>Видео. Развертывание защищенной структуры

> [!VIDEO https://www.microsoft.com/videoplayer/embed/dcd8e99f-36f1-4bc8-b3d2-9576da38d9f1?autoplay=false]

## <a name="deployment-tasks-for-guarded-fabrics-and-shielded-vms"></a>Задачи развертывания для защищенных структур и экранированных виртуальных машин

Следующая таблица разделяет задачи на развертывание защищенной структуры и создание экранированных виртуальных машин в соответствии с разными ролями администратора. Обратите внимание, что когда администратор HGS настраивает HGS с полномочными узлами Hyper-V, администратор структуры будет одновременно получать и предоставлять идентифицирующие сведения о узлах.

| Шаг и ссылка на содержимое | Образ — |
|--|--|--|
| 1. [Проверка предварительных требований для HGS](guarded-fabric-prepare-for-hgs.md) | ![Шаг 1. Проверка предварительных требований](../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png) |
| 2. [Настройка первого узла HGS](guarded-fabric-choose-where-to-install-hgs.md) | ![Шаг 2. Настройка первого узла HGS](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-first-hgs-node.png) |
| 3. [Настройка дополнительных узлов HGS](guarded-fabric-configure-additional-hgs-nodes.md) | ![Шаг 3. Настройка дополнительных узлов HGS](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-secondary-hgs-nodes.png) |
| 4. [Настройка структуры DNS](guarded-fabric-configuring-fabric-dns.md) | ![Шаг 4. Настройка структуры DNS](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-fabric-dns.png) |
| 5. [Проверка предварительных требований к узлу (ключ)](guarded-fabric-guarded-host-prerequisites.md#host-key-attestation) и [Проверка необходимых компонентов (TPM)](guarded-fabric-guarded-host-prerequisites.md#tpm-trusted-attestation) | ![Шаг 5. Проверка ключа необходимых компонентов узла и необходимого в нем TPM](../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png) |
| 6. [Создание ключа узла (Key)](guarded-fabric-create-host-key.md) и[Получение сведений об узле (TPM)](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md) | ![Шаг 6, создание ключа узла и получение сведений об узле](../media/Guarded-Fabric-Shielded-VM/guarded-host-collect-info-from-hosts.png) |
| 7. [Настройка HGS со сведениями об узле](guarded-fabric-add-host-information-to-hgs.md) | ![Шаг 7. Добавление сведений об узле в HGS](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-hgs-with-host-info.png) |
| 8. [подтверждение того, что узлы могут](guarded-fabric-confirm-hosts-can-attest-successfully.md) подтверждать | ![Шаг 8, подтвердите, что узел может подтвердить аттестацию](../media/Guarded-Fabric-Shielded-VM/guarded-host-confirm-hosts-attest.png) |
| 9. [Настройка VMM (необязательно)](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview) | ![Шаг 9. Настройка VMM (необязательно)](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-vmm.png) |
| 10. [Создание дисков шаблонов](guarded-fabric-create-a-shielded-vm-template.md) | ![Шаг 10. Создание дисков шаблонов](../media/Guarded-Fabric-Shielded-VM/guarded-host-create-template-disk.png) |
| 11. [Создание вспомогательного диска экранирования виртуальных машин для VMM (необязательно)](guarded-fabric-vm-shielding-helper-vhd.md) | ![Шаг 11. Создание диска справки экранирования виртуальных машин для VMM](../media/Guarded-Fabric-Shielded-VM/guarded-host-create-helper-disk.png) |
| 12. [настройка Windows Azure Pack (необязательно)](guarded-fabric-shielded-vm-windows-azure-pack.md) | ![Шаг 12. Настройка Windows Azure Pack (необязательно)](../media/Guarded-Fabric-Shielded-VM/guarded-host-windows-azure-pack.png) |
| 13. [Создание файла данных экранирования](guarded-fabric-tenant-creates-shielding-data.md) | ![Шаг 13. Создание файла данных экранирования](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-file.png) |
| 14. [Создание экранированных виртуальных машин с помощью Windows Azure Pack](guarded-fabric-shielded-vm-windows-azure-pack.md) | ![Шаг 14. Создание экранированных виртуальных машин с помощью Windows Azure Pack](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png) |
| 15. [Создание экранированных виртуальных машин с помощью VMM](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-vms) | ![Шаг 15. Создание экранированных виртуальных машин с помощью VMM](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png) |

## <a name="additional-references"></a>Дополнительные ссылки

- [Защищенная структура и экранированные виртуальные машины](guarded-fabric-and-shielded-vms-top-node.md)
