---
title: Восстановление леса AD — Девисинг план восстановления леса AD
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 17381f30-55f2-4e00-977a-b701675fa4ff
ms.openlocfilehash: d6637f92dff1542837b42a1406a17555a753bf86
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972321"
---
# <a name="ad-forest-recovery---devising-an-ad-forest-recovery-plan"></a>Восстановление леса AD — Девисинг план восстановления леса AD

>Область применения: Windows Server 2016, Windows Server 2012 и 2012 R2, Windows Server 2008 и 2008 R2

В зависимости от среды и бизнес-требований вам может потребоваться выполнить все действия, описанные в этом руководстве, для выполнения успешного восстановления леса. Учитывая, что данное руководством служит только в качестве шаблона для восстановления леса, крайне важно разработать пользовательский план восстановления леса, соответствующий вашей среде, и удовлетворить потребности вашего бизнеса.

Например, в плане восстановления леса должна быть подробная схема топологии лесов. На карте должны быть перечислены все сведения о контроллерах домена, такие как их имена, роли и состояние резервного копирования, а также отношения доверия между ними. Средство, которое можно использовать для создания схемы топологии, см. в разделе [Microsoft Active Directory Topology диаграммер](https://www.microsoft.com/download/details.aspx?id=13380).

Рекомендуется по крайней мере один раз в год выполнять план восстановления леса. Кроме того, рекомендуется выполнить детализацию восстановления леса при изменении членства в группе "Администраторы предприятия" или "Администраторы домена". Это гарантирует, что ИТ-специалисты полностью распознает план восстановления леса.

## <a name="next-steps"></a>Next Steps

- [Восстановление леса AD — необходимые условия](AD-Forest-Recovery-Prerequisties.md)
- [Восстановление леса AD — Девисинг план восстановления пользовательского леса](AD-Forest-Recovery-Devising-a-Plan.md)
- [Восстановление леса AD. обнаружение проблемы](AD-Forest-Recovery-Identify-the-Problem.md)
- [Восстановление леса AD. Определение способа восстановления](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [Восстановление леса AD — выполнение начального восстановления](AD-Forest-Recovery-Perform-initial-recovery.md)
- [Восстановление леса AD — процедуры](AD-Forest-Recovery-Procedures.md)
- [Восстановление леса AD — часто задаваемые вопросы](AD-Forest-Recovery-FAQ.md)
- [Восстановление леса Active Directory. Восстановление одного домена в лесу с несколькими доменами](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)
- [Восстановление леса Active Directory — восстановление леса с контроллерами домена Windows Server 2003](AD-Forest-Recovery-Windows-Server-2003.md)
