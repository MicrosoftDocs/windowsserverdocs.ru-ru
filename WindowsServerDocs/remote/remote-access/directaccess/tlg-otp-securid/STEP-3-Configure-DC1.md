---
title: Шаг 3. Настройка DC1
description: 'Эта статья является частью руководства по тестовой лаборатории: демонстрация DirectAccess с проверкой подлинности OTP и RSA SecurID для Windows Server 2016.'
manager: brianlic
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 642449e9c0c6524aa053cfb73c57b69507e5f4eb
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950460"
---
# <a name="step-3-configure-dc1"></a>Шаг 3. Настройка DC1

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

DC1 выступает в качестве контроллера домена, DNS-сервера и DHCP-сервера для домена corp.contoso.com. Настройте DC1 следующим образом.

## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>Проверка того, что Пользователь1 имеет имя участника-пользователя, определенное на компьютере DC1

1.  На компьютере DC1 откройте диспетчер сервера и в левой области щелкните **AD DS** . Щелкните правой кнопкой мыши **DC1** и выберите **Active Directory пользователи и компьютеры**. На левой панели разверните **Corp. contoso. ком\усерс** и дважды щелкните Пользователь1.

2.  На вкладке **учетная запись** убедитесь, что для **имени входа пользователя** задано значение Пользователь1. В противном случае введите **Пользователь1** в поле **имя входа пользователя** .

3.  Нажмите кнопку **OK**. Закройте консоль **Active Directory — пользователи и компьютеры**.



