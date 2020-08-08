---
title: Инициализация HGS
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: e36451c90fd543ea49989e51832ab3104d4137c0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939595"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>Инициализация службы защиты узла (HGS)

>Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016

При инициализации HGS необходимо указать режим, который будет использоваться HGS для измерения работоспособности защищенных узлов. Существует два взаимоисключающих варианта. Дополнительные сведения о том, какой режим следует выбрать, см. в разделе [защищенная структура и структура планирования экранированных виртуальных машин для поставщиков услуг размещения](guarded-fabric-planning-for-hosters.md).

В следующих разделах рассматриваются шаги развертывания для каждого режима.

- [Доверенный платформенный модуль аттестации (режим TPM)](guarded-fabric-initialize-hgs-tpm-mode.md)
- [Аттестация ключа узла (режим ключей)](guarded-fabric-initialize-hgs-key-mode.md)
- [Доверенная для администраторов аттестация (режим AD)](guarded-fabric-initialize-hgs-ad-mode.md)

Эти действия следует выполнить на физическом сервере.