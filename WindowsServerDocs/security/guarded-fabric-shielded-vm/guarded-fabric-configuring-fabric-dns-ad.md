---
description: 'Дополнительные сведения: Настройка структуры DNS для защищенных узлов (AD)'
title: Настройка DNS-сервера структуры для защищенных узлов (AD)
ms.topic: article
ms.assetid: 074b6d09-f16e-49bf-b88a-377139d35067
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 29ec5a824ca16b45bc4445a7d838c71985ca6457
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049872"
---
# <a name="configure-the-fabric-dns-for-guarded-hosts-ad"></a>Настройка DNS-сервера структуры для защищенных узлов (AD)

>Область применения. Windows Server 2016


>[!IMPORTANT]
>Режим AD является устаревшим, начиная с Windows Server 2019. Для сред, в которых невозможно подтвердить аттестацию доверенного платформенного модуля, настройте [аттестацию ключа узла](guarded-fabric-initialize-hgs-key-mode.md). Аттестация ключа узла обеспечивает аналогичные гарантии в режиме AD и проще в настройке.

Администратор структуры должен настроить структуру DNS, чтобы разрешить защищенным узлам разрешать кластер HGS.
[Администратор HGS](/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs.md)должен уже настроить кластер HGS.



[!INCLUDE [Configure fabric DNS](../../../includes/guarded-fabric-configure-fabric-dns.md)]


## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Настройка DNS в HGS и одностороннего отношения доверия](guarded-fabric-configure-dns-forwarding-and-trust.md)
