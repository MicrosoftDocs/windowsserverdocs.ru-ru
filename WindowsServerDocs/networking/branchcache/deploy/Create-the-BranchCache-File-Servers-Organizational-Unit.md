---
title: Создание подразделения файловых серверов BranchCache
description: Узнайте, как создать подразделение (OU) в домен Active Directory Services (AD DS) для файловых серверов BranchCache.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: lizross
author: eross-msft
ms.openlocfilehash: fd54492766ef157bb07e2ca3f9efbf4d644e60f6
ms.sourcegitcommit: 029b1e19ce11160d5f988046e04a83e8ab5a60dc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97904859"
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>Создание подразделения файловых серверов BranchCache

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Эту процедуру можно использовать для создания подразделения (OU) в домен Active Directory Services (AD DS) для файловых серверов BranchCache.

Минимальным требованием для выполнения этой процедуры является членство в группе **Администраторы домена** или аналогичной.

### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>Создание подразделения файловых серверов BranchCache

1.  На компьютере, где установлен AD DS, в диспетчер сервера щелкните **средства**, а затем — **Active Directory пользователи и компьютеры**. Откроется консоль Active Directory пользователи и компьютеры.

2.  В консоли Active Directory пользователи и компьютеры щелкните правой кнопкой мыши домен, в который нужно добавить подразделение. Например, если домен называется example.com, щелкните правой кнопкой мыши **example.com**. Выберите команду **Создать** и щелкните **Подразделение**. Откроется диалоговое окно **новый объект — организационное подразделение** .

3.  В диалоговом окне **новый объект — организационное подразделение** в поле **имя** введите имя нового подразделения. Например, если вы хотите присвоить имя серверам файловых серверов BranchCache, введите **BranchCache File Servers** и нажмите кнопку **ОК**.



