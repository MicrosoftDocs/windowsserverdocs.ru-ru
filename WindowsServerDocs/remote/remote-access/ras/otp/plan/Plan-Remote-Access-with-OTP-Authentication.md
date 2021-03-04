---
title: Планирование удаленного доступа с проверкой подлинности OTP
description: Узнайте о шагах настройки, необходимых для развертывания одного многосайтового развертывания Windows Server 2016 или Windows Server 2012 с удаленным доступом.
manager: brianlic
ms.topic: article
ms.assetid: 762bc463-eead-46ac-8b90-32355743c27c
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 46f75e04c64d629a09f24a781f6e136234b93967
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101803171"
---
# <a name="plan-remote-access-with-otp-authentication"></a>Планирование удаленного доступа с проверкой подлинности OTP

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

 Windows Server 2016 и Windows Server 2012 объединяют VPN DirectAccess и службы маршрутизации и удаленного доступа (RRAS) в одну роль удаленного доступа. В этом обзоре приводятся общие сведения о шагах настройки, необходимых для развертывания одного многосайтового развертывания Windows Server 2016 или Windows Server 2012 с удаленным доступом.


-  Шаг 1. [развертывание одного сервера DirectAccess с дополнительными параметрами](../../../directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings.md). Этот шаг включает планирование инфраструктуры, необходимой для развертывания одного сервера. Он включает в себя планирование параметров сети и сервера, требования к сертификатам, параметры DNS, развертывание сервера сетевого расположения, серверы управления DirectAccess, параметры Active Directory и объекты групповая политика (GPO).

-   [Шаг 2. Планирование развертывания сервера RADIUS](Step-2-Plan-the-RADIUS-Server-Deployment.md)

-   [Шаг 3. Планирование развертывания сертификатов OTP](Step-3-Plan-OTP-Certificate-Deployment.md)

-   [Шаг 4. Планирование OTP на сервере удаленного доступа](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)

После завершения этих этапов планирования см. раздел [Настройка удаленного доступа с использованием проверки подлинности OTP](../configure/configure-ra-with-otp-authentication.md). Сведения о настройке многосайтового развертывания в качестве подтверждения концепции в лабораторной среде см. в разделе [руководство по тестированию: демонстрация DirectAccess с проверкой подлинности OTP и RSA SecurID](../../../directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid.md).

