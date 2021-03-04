---
title: Шаг 3. Настройка DC1
description: Узнайте, как проверить, имеет ли Пользователь1 имя участника-пользователя, определенное на компьютере DC1.
manager: brianlic
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 0f7f283b6a7f44a800a764414870a46e3305c256
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101832733"
---
# <a name="step-3-configure-dc1"></a>Шаг 3. Настройка DC1

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

DC1 выступает в качестве контроллера домена, DNS-сервера и DHCP-сервера для домена corp.contoso.com. Настройте DC1 следующим образом.

## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>Проверка того, что Пользователь1 имеет имя участника-пользователя, определенное на компьютере DC1

1.  На компьютере DC1 откройте диспетчер сервера и в левой области щелкните **AD DS** . Щелкните правой кнопкой мыши **DC1** и выберите **Active Directory пользователи и компьютеры**. На левой панели разверните **Corp. contoso. ком\усерс** и дважды щелкните Пользователь1.

2.  На вкладке **учетная запись** убедитесь, что для **имени входа пользователя** задано значение Пользователь1. В противном случае введите **Пользователь1** в поле **имя входа пользователя** .

3.  Нажмите кнопку **ОК**. Закройте консоль **Active Directory — пользователи и компьютеры**.



