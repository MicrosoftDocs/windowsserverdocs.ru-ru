---
description: Дополнительные сведения см. в статье Настройка правил утверждений в AD FS для Windows Server.
ms.assetid: 9cafa3e1-8118-4a75-a7c2-1dbe40b1a444
title: Настройка правил утверждений
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: edf9e7c2bdcb93e3f838addf3149d06a3c632fc1
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97045442"
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
