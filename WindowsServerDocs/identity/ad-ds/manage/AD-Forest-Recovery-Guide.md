---
ms.assetid: 680e05ac-f9be-4b07-a9f4-cd6da5835952
title: Active Directory рекомендации по восстановлению леса
description: Это руководство содержит рекомендации по резервному копированию, восстановлению и аварийному восстановлению Active Directory.
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.openlocfilehash: 68acf07288ffb444dca9ca4e0edb661d41f2065c
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93071316"
---
# <a name="active-directory-forest-recovery-guide"></a>Active Directory рекомендации по восстановлению леса

>Область применения: Windows Server 2016, Windows Server 2012 и 2012 R2, Windows Server 2008 и 2008 R2, Windows Server 2003

В этом руководством содержатся рекомендации по восстановлению Active Directory® лесу, если при сбое в масштабе леса все контроллеры домена в лесу не могут функционировать нормально. Содержащиеся в нем действия служат шаблоном для плана восстановления леса, который можно настроить для конкретной среды. Эти действия применимы к контроллерам домена под управлением операционных систем Microsoft® Windows Server 2016, 2012 R2, 2012, 2008 R2, 2008 и 2003.

> [!NOTE]
> Процедуры, которые являются уникальными для контроллеров домена под управлением Windows Server 2003, объединены в [лес Active Directory восстановление Windows server 2003](AD-Forest-Recovery-Windows-Server-2003.md).

## <a name="steps-outlined-in-this-guide"></a>Действия, описанные в этом руководстве

- [Восстановление леса AD — необходимые условия](AD-Forest-Recovery-Prerequisties.md)
- [Восстановление леса AD — Девисинг план восстановления пользовательского леса](AD-Forest-Recovery-Devising-a-Plan.md)
- [Восстановление леса AD — действия по восстановлению](AD-Forest-Recovery-Steps-For-Restoring.md)
- [Восстановление леса AD. обнаружение проблемы](AD-Forest-Recovery-Identify-the-Problem.md)
- [Восстановление леса AD. Определение способа восстановления](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [Восстановление леса AD — выполнение начального восстановления](AD-Forest-Recovery-Perform-initial-recovery.md)
- [Восстановление леса AD — процедуры](AD-Forest-Recovery-Procedures.md)
- [Восстановление леса AD — часто задаваемые вопросы](AD-Forest-Recovery-FAQ.md)
- [Восстановление леса Active Directory. Восстановление одного домена в лесу с несколькими доменами](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)
- [Восстановление леса AD — виртуализация](AD-Forest-Recovery-Virtualization.md)
- [Восстановление леса Active Directory — восстановление леса с контроллерами домена Windows Server 2003](AD-Forest-Recovery-Windows-Server-2003.md)
