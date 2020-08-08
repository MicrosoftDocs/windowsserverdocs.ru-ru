---
title: Инициализация HGS с помощью аттестации, доверенной администратором
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: a3015c6af72b8a574ed1152198212b42618bb0fa
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953470"
---
# <a name="initialize-hgs-using-admin-trusted-attestation"></a>Инициализация HGS с помощью аттестации, доверенной администратором

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

>[!IMPORTANT]
>Служба аттестации, доверенная для администраторов (режим AD), устарела, начиная с Windows Server 2019. Для сред, в которых невозможно подтвердить аттестацию доверенного платформенного модуля, настройте [аттестацию ключа узла](guarded-fabric-initialize-hgs-key-mode.md). Аттестация ключа узла обеспечивает аналогичные гарантии в режиме AD и проще в настройке.


Эти действия зависят от того, инициализируется ли HGS в новом или существующем лесу бастиона:

1. [Инициализация кластера HGS в новом лесу (по умолчанию)](guarded-fabric-initialize-hgs-ad-mode-default.md)

   -Или-

   [Инициализация кластера HGS в существующем лесу бастиона](guarded-fabric-initialize-hgs-ad-mode-bastion.md)

2. [Настройка пересылки DNS в домене структуры](guarded-fabric-configuring-fabric-dns.md)

3. [Настройка перенаправления DNS и одностороннего доверия в домене HGS](guarded-fabric-configure-dns-forwarding-and-trust.md)



