---
title: Шаг 2. Планирование развертывания сервера RADIUS
description: Эта статья является частью руководств по развертыванию удаленного доступа с помощью проверки подлинности OTP в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 2d6ad863-02a5-49b0-9aff-d189e78b2b80
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c5a331e5e3ce436ac1b9727556288f2143860d9c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87968971"
---
# <a name="step-2-plan-the-radius-server-deployment"></a>Шаг 2. Планирование развертывания сервера RADIUS

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

После развертывания одного сервера удаленного доступа запланируйте сервер проверки подлинности одноразового пароля (OTP).

|Задача|Описание|
|----|--------|
|2,1. Планирование сервера RADIUS|Для сервера проверки подлинности OTP удаленный доступ в Windows Server 2016 и Windows Server 2012 поддерживает любой сервер OTP с поддержкой RADIUS, поддерживающий протокол проверки пароля (PAP).|

## <a name="21-plan-the-radius-server"></a><a name="BKMK_1.1"></a>2,1. Планирование сервера RADIUS
При планировании RADIUS-сервера для проверки подлинности OTP Обратите внимание на следующее:

-   Для большинства типов развертываний OTP необходимо настроить сервер удаленного доступа в качестве агента RADIUS. Дополнительные сведения см. в документации по поставщику OTP.

-   Для всех развертываний OTP необходимо синхронизировать Active Directory пользователей с сервером RADIUS.

-   Сервер RADIUS не обязательно должен быть членом домена.

-   При развертывании сервера RADIUS настраивается общий секрет и номер порта для трафика RADIUS. Запишите эти сведения. они необходимы при настройке сервера удаленного доступа.

Пример лабораторного руководства по тестированию, который настраивает проверку подлинности OTP с помощью сервера RSA SecurID, можно просмотреть в разделе [руководство по тестированию: демонстрация DirectAccess с проверкой подлинности OTP и RSA SecurID](../../../directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid.md).



