---
ms.assetid: 9cafa3e1-8118-4a75-a7c2-1dbe40b1a444
title: Настройка правил утверждений
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a7304402b4be1710fbff9e29e2dd0094ba621095
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864299"
---
# <a name="configure-claim-rules-in-ad-fs-for-windows-server"></a>Настройка правил утверждений в AD FS для Windows Server

В \- модели удостоверений на основе утверждений функция службы федерации Active Directory (AD FS) \( AD FS в \) качестве служб федерации, — выдача маркера, содержащего набор утверждений. Правила утверждений управляют решениями относительно утверждений, которые AD FS проблемы. Правила утверждений и все данные конфигурации сервера хранятся в базе данных конфигурации AD FS.  
  
AD FS принимает решения на выдачу на основе сведений об удостоверениях, предоставленных ему в виде утверждений и других контекстных сведений. На высоком уровне AD FS работает как обработчик правил, используя один набор заявок в качестве входных данных, выполняет ряд преобразований, а затем возвращает другой набор заявок в качестве выходных данных. 

Следующие разделы помогут вам создать правила, которые AD FS будет обрабатывать: 
  
-   [Создание правила для передачи или фильтрации входящего утверждения](Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [Создание правила для разрешения всем пользователям](Create-a-Rule-to-Permit-All-Users.md)  
  
-   [Создание правила для разрешения или запрета пользователям на основе входящего утверждения](Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [Создание правила для отправки атрибутов LDAP в качестве утверждений](Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [Создание правила для отправки членства в группе в качестве утверждения](Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [Создание правила для преобразования входящего утверждения](Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [Создание правила для отправки утверждения методов аутентификации](Create-a-Rule-to-Send-an-Authentication-Method-Claim.md) 
-   [Создание правила для отправки утверждения, совместимого с AD FS 1. x](Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md) 
  
-   [Создание правила для отправки утверждений с помощью настраиваемого правила](Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)  

## <a name="see-also"></a>См. также:  
[Операции AD FS](../ad-fs-operations.md) 
