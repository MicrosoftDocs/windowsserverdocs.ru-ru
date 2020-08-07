---
title: Восстановление леса AD — сброс учетной записи компьютера на контроллере домена
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.openlocfilehash: 3d779e989c4414629c9a7414adf41c96525368c4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969841"
---
# <a name="ad-forest-recovery---resetting-the-computer-account-on-the-dc"></a>Восстановление леса AD — сброс учетной записи компьютера на контроллере домена

>Область применения: Windows Server 2016, Windows Server 2012 и 2012 R2, Windows Server 2008 и 2008 R2

 Используйте следующую процедуру, чтобы сбросить пароль учетной записи компьютера для контроллера домена.

## <a name="to-reset-the-computer-account-password-of-the-domain-controller"></a>Сброс пароля учетной записи компьютера контроллера домена

1. В командной строке введите следующую команду и нажмите клавишу ВВОД:

   ```
   netdom help resetpwd
   ```

2. Используйте синтаксис, который эта команда предоставляет для использования программы командной строки Netdom для сброса пароля учетной записи компьютера, например:

   ```
   netdom resetpwd /server:domain controller name /userD:administrator /passwordd:*
   ```

    Где *имя контроллера домена* — это локальный DC, который восстанавливается.

   > [!NOTE]
   > Эту команду следует выполнять дважды.

## <a name="next-steps"></a>Next Steps

- [Руководство по восстановлению леса AD](AD-Forest-Recovery-Guide.md)
- [Восстановление леса AD — процедуры](AD-Forest-Recovery-Procedures.md)
