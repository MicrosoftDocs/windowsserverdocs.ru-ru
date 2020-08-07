---
title: Создание подразделения файловых серверов BranchCache
description: Эта статья является частью руководства по развертыванию BranchCache для Windows Server 2016, в котором показано, как развернуть BranchCache в распределенном и размещенном режимах кэша для оптимизации использования пропускной способности глобальной сети в филиалах.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 01b1efe79eb06ba25af93b6cec224cc05c016cc6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971891"
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>Создание подразделения файловых серверов BranchCache

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Эту процедуру можно использовать для создания подразделения (OU) в домен Active Directory Services (AD DS) для файловых серверов BranchCache.

Минимальным требованием для выполнения этой процедуры является членство в группе **Администраторы домена** или аналогичной.

### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>Создание подразделения файловых серверов BranchCache

1.  На компьютере, где установлен AD DS, в диспетчер сервера щелкните **средства**, а затем — **Active Directory пользователи и компьютеры**. Откроется консоль Active Directory пользователи и компьютеры.

2.  В консоли Active Directory пользователи и компьютеры щелкните правой кнопкой мыши домен, в который нужно добавить подразделение. Например, если домен называется example.com, щелкните правой кнопкой мыши **example.com**. Выберите команду **Создать** и щелкните **Подразделение**. Откроется диалоговое окно **новый объект — организационное подразделение** .

3.  В диалоговом окне **новый объект — организационное подразделение** в поле **имя**введите имя нового подразделения. Например, если вы хотите присвоить имя серверам файловых серверов BranchCache, введите **BranchCache File Servers**и нажмите кнопку **ОК**.



