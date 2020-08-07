---
title: Добавление сведений об узле для аттестации, доверенной для администраторов
ms.topic: article
ms.assetid: 87089ebc-b953-4aa3-96b5-966cf91acb02
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: abc01dbb691843d199169bd654afaa5cf06bbb87
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971441"
---
# <a name="authorize-hyper-v-hosts-using-admin-trusted-attestation"></a>Авторизация узлов Hyper-V с помощью аттестации, доверенной для администраторов

> Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

> [!IMPORTANT]
> Служба аттестации, доверенная для администраторов (режим AD), устарела, начиная с Windows Server 2019. Для сред, в которых невозможно подтвердить аттестацию доверенного платформенного модуля, настройте [аттестацию ключа узла](guarded-fabric-initialize-hgs-key-mode.md). Аттестация ключа узла обеспечивает аналогичные гарантии в режиме AD и проще в настройке.


Авторизация защищенного узла в режиме AD:

1. В домене структуры добавьте узлы Hyper-V в группу безопасности.
2. В домене HGS Зарегистрируйте идентификатор безопасности группы безопасности с помощью HGS.

## <a name="add-the-hyper-v-host-to-a-security-group-and-reboot-the-host"></a>Добавление узла Hyper-V в группу безопасности и перезагрузка узла

1. Создайте **глобальную** группу безопасности в домене структуры и добавьте узлы Hyper-V, которые будут запускать экранированные виртуальные машины.
   Перезапустите узлы, чтобы обновить их принадлежность к группам.

2. Используйте Get-ADGroup, чтобы получить идентификатор безопасности (SID) группы безопасности и предоставить ее администратору HGS.

   ```powershell
   Get-ADGroup "Guarded Hosts"
   ```

   ![Команда Get-AdGroup с OUTPUT](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>Регистрация идентификатора безопасности группы безопасности в HGS

1. Получите идентификатор безопасности группы безопасности для защищенных узлов от администратора структуры и выполните следующую команду, чтобы зарегистрировать группу безопасности в HGS.
   Повторно выполните команду, если это необходимо для дополнительных групп.
   Укажите понятное имя для группы.
   Оно не обязательно должно совпадать с именем группы безопасности Active Directory.

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. Чтобы проверить, добавлена ли группа, выполните команду [Get-хгсаттестатионхостграуп](https://technet.microsoft.com/library/mt652172.aspx).


