---
title: Шаг 3. Проверка расширенного развертывания DirectAccess
description: Узнайте, как проверить правильность настройки расширенного развертывания DirectAccess.
manager: brianlic
ms.topic: article
ms.assetid: ae8bbff0-c981-4bc6-8df1-861621d0627f
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 38e93e9c40b1e87557bd077f7b9d2129a2e9bae4
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97949820"
---
# <a name="step-3-verify-the-advanced-directaccess-deployment"></a>Шаг 3. Проверка расширенного развертывания DirectAccess

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе описывается, как проверить правильность настройки развертывания DirectAccess.

### <a name="to-verify-access-to-internal-resources-through-directaccess"></a>Проверка доступа к внутренним ресурсам с помощью DirectAccess

1.  Подключите клиентский компьютер DirectAccess к корпоративной сети и получите объект групповая политика.

2.  Щелкните значок **Сетевые подключения** в области уведомлений, чтобы получить доступ к диспетчеру носителей DirectAccess.

3.  Щелкните **подключение DirectAccess**, и вы увидите, что состояние **подключено локально**.

4.  Подключите клиентский компьютер к внешней сети и попытайтесь получить доступ к внутренним ресурсам.

    Вам должны быть доступны все корпоративные ресурсы.

## <a name="previous-step"></a><a name="BKMK_Links"></a>Предыдущий шаг

-   [Шаг 2. Настройка серверов DirectAccess](./da-adv-configure-s2-servers.md)