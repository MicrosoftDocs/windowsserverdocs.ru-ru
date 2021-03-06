---
title: Создание подразделения файловых серверов BranchCache
description: Узнайте, как создать подразделение (OU) в домен Active Directory Services (AD DS) для файловых серверов BranchCache.
manager: brianlic
ms.topic: how-to
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: jgerend
author: JasonGerend
ms.date: 01/05/2021
ms.openlocfilehash: f5b94681731504f520acd597ec90ef6f52e06fc5
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101828773"
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>Создание подразделения файловых серверов BranchCache

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Эту процедуру можно использовать для создания подразделения (OU) в домен Active Directory Services (AD DS) для файловых серверов BranchCache.

Минимальным требованием для выполнения этой процедуры является членство в группе **Администраторы домена** или аналогичной.

### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>Создание подразделения файловых серверов BranchCache

1.  На компьютере, где установлен AD DS, в диспетчер сервера щелкните **средства**, а затем — **Active Directory пользователи и компьютеры**. Откроется консоль Active Directory пользователи и компьютеры.

2.  В консоли Active Directory пользователи и компьютеры щелкните правой кнопкой мыши домен, в который нужно добавить подразделение. Например, если домен называется example.com, щелкните правой кнопкой мыши **example.com**. Выберите команду **Создать** и щелкните **Подразделение**. Откроется диалоговое окно **новый объект — организационное подразделение** .

3.  В диалоговом окне **новый объект — организационное подразделение** в поле **имя** введите имя нового подразделения. Например, если вы хотите присвоить имя серверам файловых серверов BranchCache, введите **BranchCache File Servers** и нажмите кнопку **ОК**.



