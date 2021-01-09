---
title: Шаг 8. Настройка INET1
description: Узнайте, как настроить запись DNS для 2-EDGE1 на INET1.
ms.topic: article
ms.assetid: 693acb5c-dffc-4484-8286-163bb67724c9
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 08/07/2020
ms.openlocfilehash: 0a17e726d200cc344c83f2d4aafed2f5493b294a
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2021
ms.locfileid: "98040374"
---
# <a name="step-8-configure-inet1"></a>ШАГ 8. Настройка INET1

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

Чтобы разрешить клиентским компьютерам подключаться к серверам удаленного доступа через Интернет, необходимо настроить запись DNS для 2-EDGE1 в INET1.

### <a name="to-create-the-2-edge1-dns-entry"></a>Создание записи DNS 2-EDGE1

1.  На **начальном** экране введите **днсмгмт. msc** и нажмите клавишу ВВОД.

2.  В дереве консоли откройте **зоны прямого просмотра**, щелкните **contoso.com**, щелкните правой кнопкой мыши **contoso.com**, а затем выберите **новый узел (A или AAAA)**.

3.  В списке **имя** введите **2-EDGE1**. В списке **IP-адрес** введите **131.107.0.20**. Щелкните **Добавить узел**, после чего нажмите **OK**, а затем — **Готово**.



