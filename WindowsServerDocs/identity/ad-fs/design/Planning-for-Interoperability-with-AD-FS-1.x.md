---
description: Дополнительные сведения см. в статье Планирование взаимодействия с AD FS 1. x.
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: Планирование взаимодействия со службами федерации Active Directory 1.x
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: e956d66dd528ed73e4adcdfb8d9d04f4cab1666d
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049702"
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>Планирование взаимодействия со службами федерации Active Directory 1.x

Службы федерации Active Directory (AD FS) \( AD FS \) серверы федерации под windows Server &reg; 2012 могут взаимодействовать с AD FS 1,0, \( установленным с windows Server 2003 R2 \) Служба федерации, и AD FS 1,1, \( установленным с windows Server 2008 или Windows Server 2008 R2 \) Служба федерации. Поддерживаются любые из указанных ниже сочетаний.

-   Любой AD FS 1. *x* служба федерации может отправить утверждение, которое может использоваться AD FS Служба федерации в Windows Server 2012. Дополнительные сведения см. [в разделе Контрольный список: настройка AD FS для использования утверждений от AD FS 1. x](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md).

-   Любой AD FS служба федерации в Windows Server 2012 может отправить AD FS 1. *x* \- совместимое утверждение, которое может быть использовано AD FS 1. *x* служба Федерации. Дополнительные сведения см. в разделе [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Federation Service](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md).

-   Любой AD FS служба федерации в Windows Server 2012 может отправить AD FS 1. *x* \- совместимое утверждение, которое может быть использовано одним или несколькими веб-серверами, на которых работает AD FS 1.  \- веб-агент x с поддержкой утверждений. Дополнительные сведения см. в разделе [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Claims-Aware Web Agent](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md).

> [!NOTE]
> AD FS не поддерживает и не взаимодействуют с AD FS 1. Веб-агент *x* Windows NT на основе маркеров.

AD FS 1. *x* \- совместимое утверждение — это утверждение, которое может быть отправлено служба федерацииом AD FS в Windows Server 2012 и понятным AD FS 1. *x* служба Федерации. Чтобы AD FS 1. *x* служба федерации может использовать утверждения, которые отправляет AD FS Служба федерации, \( \) необходимо отправить тип утверждения идентификатора идентификатора имени.

## <a name="understanding-the-name-id-claim-type"></a>Сведения о типе утверждений "Идентификатор имени"
Тип утверждений "Идентификатор имени" аналогичен типу утверждений удостоверений, который используется в AD FS 1.*x*. Его необходимо использовать при любом взаимодействии с AD FS 1.*x*. Тип утверждения идентификатора имени включает либо AD FS 1. *x* служба федерации или AD FS 1. *x* \- -агент с поддержкой утверждений для использования утверждений, которые AD FS в Windows Server 2012, при условии, что эти утверждения отправляются в одном из форматов идентификаторов имен, указанных в следующей таблице.


|      Формат идентификатора имени       |               Соответствующий код URI                |
|---------------------------|------------------------------------------------|
| AD FS 1. Адрес электронной почты *x* | http://schemas.xmlsoap.org/claims/EmailAddress |
|   Имя участника-пользователя электронной почты AD FS 1.*x*   |     http://schemas.xmlsoap.org/claims/UPN      |
|        Общее имя        |  http://schemas.xmlsoap.org/claims/CommonName  |
|           Группа           |    http://schemas.xmlsoap.org/claims/Group     |

Должно быть отправлено только одно утверждение типа "Идентификатор имени" в соответствующем формате. Если это условие выполнено, можно отправлять множество других утверждений с учетом ограничений, описанных в таблице.

> [!NOTE]
> AD FS 1. *x* служба федерации может интерпретировать только типы входящих утверждений, которые начинаются с URI универсального идентификатора ресурса \( \) http://schemas.xmlsoap.org/claims/ .

## <a name="see-also"></a>См. также:
[Руководство по разработке служб федерации Active Directory в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
