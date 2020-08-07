---
title: Шаг 3. Проверка развертывания
description: Этот раздел является частью руководств по удаленному управлению клиентами DirectAccess в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 6a78a078-d2e7-4cbd-b8d5-20cfb6d1524b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7e8b7e037c0c98c62daf9abdf743ae4c1153f054
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950849"
---
# <a name="step-3-verify-the-deployment"></a>Шаг 3. Проверка развертывания

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе описывается, как проверить правильность настройки развертывания для удаленного управления клиентами DirectAccess.

### <a name="to-verify-proper-deployment"></a>Проверка правильности развертывания

1.  Подключите клиентский компьютер DirectAccess к корпоративной сети и получите объект групповая политика.

2.  На клиентском компьютере щелкните значок " **Сетевые подключения** " в области уведомлений, чтобы получить доступ к диспетчеру носителей DirectAccess.

3.  Щелкните **подключение DirectAccess**, и вы увидите, что состояние **подключено локально**.

4.  Удалите компьютер из корпоративной сети и подключите его к общедоступной сети.

5.  В командной строке введите команду **nltest/dsgetdc: [полное доменное имя]**. Эта команда проверит доступность корпоративной сети для клиента. Если контроллер домена недоступен, в следующем сообщении об ошибке Отобразится сообщение о том, что домен не существует: ERROR_NO_SUCH_DOMAIN.



