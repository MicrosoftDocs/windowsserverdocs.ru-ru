---
title: Восстановление леса Active Directory — официальная синхронизация SYSVOL
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 38a1c543-c76d-4b8e-a06b-53742aaa172f
ms.openlocfilehash: 8d4df4b7b893c0c6e8fc6b467ee115e9013335f9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956901"
---
# <a name="ad-forest-recovery---performing-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>Восстановление леса Active Directory — выполнение полномочной синхронизации SYSVOL с реплицированной службой DFSR

>Область применения: Windows Server 2016, Windows Server 2012 и 2012 R2, Windows Server 2008 и 2008 R2

Существует несколько способов выполнения полномочного восстановления SYSVOL. Можно либо изменить атрибут **мсдфср-Options** , либо выполнить восстановление состояния системы с помощью WBADMIN – ауссисвол. Если имеется возможность восстановить резервную копию состояния системы (то есть восстановление AD DS на том же оборудовании и экземпляре операционной системы), то проще использовать Wbadmin – ауссисвол. Но если необходимо выполнить восстановление исходного состояния системы, необходимо изменить атрибут **мсдфср-Options** .

Выполните следующие действия, чтобы выполнить авторитетную синхронизацию SYSVOL (если она реплицируется с помощью DFSR), изменив атрибут **мсдфср-Options** . Если SYSVOL реплицируется с помощью FRS, см. [статью 290762](https://go.microsoft.com/fwlink/?LinkId=148443).

## <a name="to-perform-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>Выполнение полномочной синхронизации SYSVOL, реплицированной с помощью DFSR

1. Откройте оснастку "Пользователи и компьютеры Active Directory".
2. Щелкните **вид**, а затем выберите **Пользователи, контакты, группы и компьютеры в качестве контейнеров** и **дополнительных функций**.

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol1.png)

3. В представлении дерева щелкните **контроллеры домена**, имя ВОССТАНАВЛИВАЕМого контроллера домена, **DFSR-LocalSettings**, а затем — **системный том домена**.

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol2.png)

4. В области сведений щелкните правой кнопкой мыши элемент **Подписка SYSVOL**, выберите пункт **Свойства**и щелкните **Редактор атрибутов**.

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol3.png)

5. Щелкните **мсдфср-Options**, щелкните **изменить**, введите **1**и нажмите кнопку **ОК** .

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol4.png)

6. Нажмите кнопку **ОК** , чтобы закрыть редактор атрибутов.

## <a name="next-steps"></a>Next Steps

- [Руководство по восстановлению леса AD](AD-Forest-Recovery-Guide.md)
- [Восстановление леса AD — процедуры](AD-Forest-Recovery-Procedures.md)
