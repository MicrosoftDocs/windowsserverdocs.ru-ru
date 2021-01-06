---
title: Включение возможности публикации хэша для файловых серверов, входящих в домен
description: Узнайте, как включить публикацию хэша BranchCache для нескольких файловых серверов.
manager: brianlic
ms.topic: get-started-article
ms.assetid: a3f1f7c4-d9b2-43e6-8bfa-fac707bbd4d3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: beb6c20cf9f750ed0296b96acb6253b5352385fb
ms.sourcegitcommit: 029b1e19ce11160d5f988046e04a83e8ab5a60dc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97904819"
---
# <a name="enable-hash-publication-for-domain-member-file-servers"></a>Включение возможности публикации хэша для файловых серверов, входящих в домен

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

При использовании домен Active Directory Services (AD DS) можно использовать групповая политика домена, чтобы включить публикацию хэша BranchCache для нескольких файловых серверов. Для этого необходимо создать подразделение, добавить файловые серверы в подразделение, создать публикацию хэша BranchCache групповая политика объект (GPO), а затем настроить объект групповой политики.

Сведения о включении публикации хэша для нескольких файловых серверов см. в следующих разделах.

-   [Создание подразделения файловых серверов BranchCache](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)

-   [Перемещение файловых серверов в подразделение файловых серверов BranchCache](../../branchcache/deploy/Move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)

-   [Создание объекта групповой политики публикации хэша BranchCache](../../branchcache/deploy/Create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)

-   [Настройка объекта групповой политики публикации хэша BranchCache](../../branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)



