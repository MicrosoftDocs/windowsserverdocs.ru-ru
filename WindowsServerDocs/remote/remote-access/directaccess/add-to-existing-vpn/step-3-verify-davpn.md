---
title: Шаг 3. Проверка развертывания с помощью удаленного доступа (VPN)
description: Узнайте, как проверить правильность настройки развертывания DirectAccess.
manager: brianlic
ms.topic: article
ms.assetid: 43ac612e-2e77-418c-8171-ebb2086b7cb6
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 75ca3194132b8869d40b40e150eb9ae7fe9a6376
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947030"
---
# <a name="step-3-verify-the-remote-access-vpn-deployment"></a>Шаг 3. Проверка развертывания с помощью удаленного доступа (VPN)

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе описывается, как проверить правильность настройки развертывания DirectAccess.

### <a name="to-verify-access-to-internal-resources-through-directaccess"></a>Проверка доступа к внутренним ресурсам с помощью DirectAccess

1.  Подключите клиентский компьютер с DirectAccess к корпоративной сети и получите групповую политику.

2.  В области уведомлений щелкните значок **Сетевые подключения**, чтобы получить доступ к диспетчеру мультимедиа DA.

3.  Щелкните **Подключение DirectAccess**. Будет отображено состояние подключения — **Подключено локально**.

4.  Подключите клиентский компьютер к внешней сети и попытайтесь получить доступ к внутренним ресурсам.

    Вам должны быть доступны все корпоративные ресурсы.



