---
title: Включение возможности публикации хэша для файловых серверов, входящих в домен
description: Эта статья является частью руководства по развертыванию BranchCache для Windows Server 2016, в котором показано, как развернуть BranchCache в распределенном и размещенном режимах кэша для оптимизации использования пропускной способности глобальной сети в филиалах.
manager: brianlic
ms.topic: get-started-article
ms.assetid: a3f1f7c4-d9b2-43e6-8bfa-fac707bbd4d3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: df03945a80ae86aad91a004ea710ac6eff10c3ad
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971861"
---
# <a name="enable-hash-publication-for-domain-member-file-servers"></a>Включение возможности публикации хэша для файловых серверов, входящих в домен

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

При использовании домен Active Directory Services (AD DS) можно использовать групповая политика домена, чтобы включить публикацию хэша BranchCache для нескольких файловых серверов. Для этого необходимо создать подразделение, добавить файловые серверы в подразделение, создать публикацию хэша BranchCache групповая политика объект (GPO), а затем настроить объект групповой политики.

Сведения о включении публикации хэша для нескольких файловых серверов см. в следующих разделах.

-   [Создание подразделения файловых серверов BranchCache](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)

-   [Перемещение файловых серверов в подразделение файловых серверов BranchCache](../../branchcache/deploy/Move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)

-   [Создание объекта групповой политики публикации хэша BranchCache](../../branchcache/deploy/Create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)

-   [Настройка объекта групповой политики публикации хэша BranchCache](../../branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)



