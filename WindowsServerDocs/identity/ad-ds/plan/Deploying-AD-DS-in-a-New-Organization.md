---
ms.assetid: a589dda6-e05b-4b44-ae3e-b15dd3877617
title: Развертывание доменных служб Active Directory в новой организации
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ba7fdf5bd2e14e7340e9ef7de93747c1c6c666da
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822647"
---
# <a name="deploying-ad-ds-in-a-new-organization"></a>Развертывание доменных служб Active Directory в новой организации

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Тщательное подготовка структуры домен Active Directory служб (AD DS) очень важно для экономичного развертывания. Если сетевая среда в данный момент работает без службы каталогов, перед развертыванием AD DS завершите комплексную структуру AD DS логической структуры. Затем можно развернуть новый корневой домен леса и развернуть оставшуюся часть структуры домена в соответствии с вашими макетами.  
  
На следующем рисунке показаны шаги для развертывания Windows Server 2008 AD DS в сетевой среде, работающей в данный момент без службы каталогов.  
  
![развертывание в новой Организации](media/Deploying-AD-DS-in-a-New-Organization/daa38971-86f2-4033-9442-0cdff9ecc48f.gif)  
  
Список подробных задач, которые можно использовать для планирования и развертывания AD DS в новой организации, см. в разделе [Контрольный список: развертывание AD DS в новой организации](https://technet.microsoft.com/library/cc725897.aspx).  
  


