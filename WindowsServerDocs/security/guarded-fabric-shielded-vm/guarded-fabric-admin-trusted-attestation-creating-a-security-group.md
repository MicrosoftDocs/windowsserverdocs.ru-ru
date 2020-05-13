---
title: Создание группы безопасности для защищенных узлов и регистрация группы с помощью HGS
ms.prod: windows-server
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: b6fac7792b91e7415d0714b43201c404da2155bf
ms.sourcegitcommit: 32f810c5429804c384d788c680afac427976e351
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2020
ms.locfileid: "83203403"
---
# <a name="create-a-security-group-for-guarded-hosts-and-register-the-group-with-hgs"></a>Создание группы безопасности для защищенных узлов и регистрация группы с помощью HGS

> Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

> [!IMPORTANT]
> Режим AD является устаревшим, начиная с Windows Server 2019. Для сред, в которых невозможно подтвердить аттестацию доверенного платформенного модуля, настройте [аттестацию ключа узла](guarded-fabric-initialize-hgs-key-mode.md). Аттестация ключа узла обеспечивает аналогичные гарантии в режиме AD и проще в настройке.

В этом разделе описываются промежуточные шаги по подготовке узлов Hyper-V к защищенным узлам с помощью аттестации, доверенной для администраторов (режим AD). Перед выполнением этих действий выполните действия, описанные в статье [Настройка структуры DNS для узлов, которые станут защищенными узлами](guarded-fabric-configuring-fabric-dns-ad.md).


## <a name="create-a-security-group-and-add-hosts"></a>Создание группы безопасности и Добавление узлов

1. Создайте новую **глобальную** группу безопасности в домене структуры и добавьте узлы Hyper-V, которые будут запускать экранированные виртуальные машины. Перезапустите узлы, чтобы обновить их принадлежность к группам.

2. Используйте Get-ADGroup, чтобы получить идентификатор безопасности (SID) группы безопасности и предоставить ее администратору HGS.

    ```powershell
    Get-ADGroup "Guarded Hosts"
    ```

    ![Команда Get-AdGroup с OUTPUT](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>Регистрация идентификатора безопасности группы безопасности в HGS

1. На сервере HGS выполните следующую команду, чтобы зарегистрировать группу безопасности в HGS.
   Повторно выполните команду, если это необходимо для дополнительных групп.
   Укажите понятное имя для группы.
   Оно не обязательно должно совпадать с именем группы безопасности Active Directory.

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. Чтобы проверить, добавлена ли группа, выполните команду [Get-хгсаттестатионхостграуп](https://technet.microsoft.com/library/mt652172.aspx).

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Подтверждение аттестации](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="see-also"></a>См. также раздел

- [Развертывание службы защиты узла для защищенных узлов и экранированных виртуальных машин](guarded-fabric-deploying-hgs-overview.md)
