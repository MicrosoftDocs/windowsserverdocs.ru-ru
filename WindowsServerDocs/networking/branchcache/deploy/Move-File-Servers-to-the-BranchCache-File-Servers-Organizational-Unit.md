---
title: Перемещение файловых серверов в подразделение файловых серверов BranchCache
description: Эта статья является частью руководства по развертыванию BranchCache для Windows Server 2016, в котором показано, как развернуть BranchCache в распределенном и размещенном режимах кэша для оптимизации использования пропускной способности глобальной сети в филиалах.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 56c915ec-edb1-43b0-8ad2-c93841bb566f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c44fb11a2935c11474abd3b3cc39cfd0eeb34734
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962348"
---
# <a name="move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>Перемещение файловых серверов в подразделение файловых серверов BranchCache

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Эту процедуру можно использовать для добавления файловых серверов BranchCache в подразделение (OU) в домен Active Directory Services (AD DS).

Минимальным требованием для выполнения этой процедуры является членство в группе **Администраторы домена** или аналогичной.

> [!NOTE]
> Перед добавлением учетных записей компьютеров в подразделение с помощью этой процедуры необходимо создать подразделение файловых серверов BranchCache в консоли Active Directory пользователи и компьютеры. Дополнительные сведения см. [в разделе Создание подразделения файловых серверов BranchCache](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md).

### <a name="to-move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>Перемещение файловых серверов в организационное подразделение файловых серверов BranchCache

1.  На компьютере, где установлен AD DS, в диспетчер сервера щелкните **средства**, а затем — **Active Directory пользователи и компьютеры**. Откроется консоль Active Directory пользователи и компьютеры.

2.  В консоли Active Directory пользователи и компьютеры найдите учетную запись компьютера для файлового сервера BranchCache, щелкните ее левой кнопкой мыши, чтобы выбрать учетную запись, а затем перетащите учетную запись компьютера в созданном ранее подразделении файловых серверов BranchCache. Например, если вы ранее создали подразделение с именем **файловые серверы BranchCache**, перетащите учетную запись компьютера в подразделении **файловых серверов BranchCache** .

3.  Повторите предыдущий шаг для каждого файлового сервера BranchCache в домене, который необходимо переместить в подразделение.



