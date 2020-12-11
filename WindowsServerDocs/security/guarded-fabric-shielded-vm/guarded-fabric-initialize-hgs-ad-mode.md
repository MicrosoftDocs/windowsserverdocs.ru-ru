---
description: Дополнительные сведения см. в статье инициализация HGS с помощью аттестации, доверенной администратором
title: Инициализация HGS с помощью аттестации, доверенной администратором
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 65ba0bd90d42ac038eeb8eb304def80ce7093ff1
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049762"
---
# <a name="initialize-hgs-using-admin-trusted-attestation"></a>Инициализация HGS с помощью аттестации, доверенной администратором

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

>[!IMPORTANT]
>Служба аттестации, доверенная для администраторов (режим AD), устарела, начиная с Windows Server 2019. Для сред, в которых невозможно подтвердить аттестацию доверенного платформенного модуля, настройте [аттестацию ключа узла](guarded-fabric-initialize-hgs-key-mode.md). Аттестация ключа узла обеспечивает аналогичные гарантии в режиме AD и проще в настройке.


Эти действия зависят от того, инициализируется ли HGS в новом или существующем лесу бастиона:

1. [Инициализация кластера HGS в новом лесу (по умолчанию)](guarded-fabric-initialize-hgs-ad-mode-default.md)

   или

   [Инициализация кластера HGS в существующем лесу бастиона](guarded-fabric-initialize-hgs-ad-mode-bastion.md)

2. [Настройка пересылки DNS в домене структуры](guarded-fabric-configuring-fabric-dns.md)

3. [Настройка перенаправления DNS и одностороннего доверия в домене HGS](guarded-fabric-configure-dns-forwarding-and-trust.md)



