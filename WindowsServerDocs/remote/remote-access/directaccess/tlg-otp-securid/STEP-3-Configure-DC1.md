---
title: Шаг 3. Настройка DC1
description: Узнайте, как проверить, имеет ли Пользователь1 имя участника-пользователя, определенное на компьютере DC1.
manager: brianlic
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 7da9496d27b36fdcf9abedeb76f472c6a78a0866
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2021
ms.locfileid: "98040064"
---
# <a name="step-3-configure-dc1"></a>Шаг 3. Настройка DC1

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

DC1 выступает в качестве контроллера домена, DNS-сервера и DHCP-сервера для домена corp.contoso.com. Настройте DC1 следующим образом.

## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>Проверка того, что Пользователь1 имеет имя участника-пользователя, определенное на компьютере DC1

1.  На компьютере DC1 откройте диспетчер сервера и в левой области щелкните **AD DS** . Щелкните правой кнопкой мыши **DC1** и выберите **Active Directory пользователи и компьютеры**. На левой панели разверните **Corp. contoso. ком\усерс** и дважды щелкните Пользователь1.

2.  На вкладке **учетная запись** убедитесь, что для **имени входа пользователя** задано значение Пользователь1. В противном случае введите **Пользователь1** в поле **имя входа пользователя** .

3.  Нажмите **OK**. Закройте консоль **Active Directory — пользователи и компьютеры**.



