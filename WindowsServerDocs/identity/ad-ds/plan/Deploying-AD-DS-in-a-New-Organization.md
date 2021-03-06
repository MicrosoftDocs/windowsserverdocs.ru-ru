---
description: Дополнительные сведения о развертывании AD DS в новой Организации
ms.assetid: a589dda6-e05b-4b44-ae3e-b15dd3877617
title: Развертывание доменных служб Active Directory в новой организации
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 6877b1a5499d10739cef5aa7f62589416464181f
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97044112"
---
# <a name="deploying-ad-ds-in-a-new-organization"></a>Развертывание доменных служб Active Directory в новой организации

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Тщательное подготовка структуры домен Active Directory служб (AD DS) очень важно для экономичного развертывания. Если сетевая среда в данный момент работает без службы каталогов, перед развертыванием AD DS завершите комплексную структуру AD DS логической структуры. Затем можно развернуть новый корневой домен леса и развернуть оставшуюся часть структуры домена в соответствии с вашими макетами.

На следующем рисунке показаны шаги для развертывания Windows Server 2008 AD DS в сетевой среде, работающей в данный момент без службы каталогов.

![развертывание в новой Организации](media/Deploying-AD-DS-in-a-New-Organization/daa38971-86f2-4033-9442-0cdff9ecc48f.gif)

Список подробных задач, которые можно использовать для планирования и развертывания AD DS в новой организации, см. в разделе [Контрольный список: развертывание AD DS в новой организации](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc725897(v=ws.10)).

