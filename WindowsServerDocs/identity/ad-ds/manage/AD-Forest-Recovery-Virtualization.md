---
description: 'Дополнительные сведения: Виртуализация восстановления леса Active Directory'
title: Виртуализация восстановления леса Active Directory
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.openlocfilehash: bf84f5db627d2383a47a9d23ce72acbc45251ea6
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049552"
---
# <a name="active-directory-forest-recovery-virtualization"></a>Виртуализация Active Directory восстановления леса

>Область применения: Windows Server 2016, Windows Server 2012 и 2012 R2, Windows Server 2008 и 2008 R2

В этом разделе описывается функция клонирования виртуализованного контроллера домена в Windows Server 2016, 2012 R2 и 2012.

## <a name="using-virtualized-domain-controller-cloning-to-expedite-forest-recovery"></a>Использование виртуализированного клонирования контроллера домена для ускорения восстановления леса

Виртуализованное клонирование контроллера домена (DC) упрощает и ускоряет процесс установки дополнительных виртуализованных контроллеров домена в домене, особенно в централизованных расположениях, таких как центры обработки данных, в которых несколько контроллеров домена работают на низкоуровневых оболочках. После восстановления одного виртуального контроллера домена в каждом домене из резервной копии дополнительные контроллеры домена в каждом домене можно быстро перевести в оперативный режим с помощью виртуализированного процесса клонирования контроллеров домена. Вы можете подготовить первый виртуальный контроллер домена, который вы восстанавливаете, выключите его, а затем скопируйте этот виртуальный жесткий диск столько раз, сколько необходимо, чтобы создать клонированные виртуальные контроллеры доменов для создания домена.

Требования к виртуализированному клонированию контроллера домена:

- Гипервизор должен поддерживать VM-GenerationID. Hyper-V в Windows Server 2016, 2012 и Windows 8 — это пример низкоуровневой оболочки, поддерживающей VM-GenerationID. Если VM-GenerationID поддерживается, обратитесь к поставщику гипервизора.
- Виртуализованный контроллер домена, используемый в качестве источника для клонирования, должен работать под управлением Windows Server 2016 или 2012 и быть членом клонированной группы контроллеров домена.
- Эмулятор основного контроллера домена должен работать под управлением Windows Server 2016 или 2012. Эмулятор основного контроллера домена можно клонировать, если он виртуализирован.

Пошаговые инструкции по выполнению виртуализированного клонирования контроллеров домена см. в статье [Введение в виртуализацию домен Active Directory Services (AD DS) (уровень 100)](../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md). Дополнительные сведения о том, как работает виртуализированное клонирование КОНТРОЛЛЕРов домена, см. в статье [техническое руководство по виртуализированному контроллеру доменов (уровень 300)](../deploy/virtual-dc/virtualized-domain-controller-technical-reference--level-300-.md).

## <a name="next-steps"></a>Дальнейшие действия

- [Восстановление леса AD — необходимые условия](AD-Forest-Recovery-Prerequisties.md)
- [Восстановление леса AD — Девисинг план восстановления пользовательского леса](AD-Forest-Recovery-Devising-a-Plan.md)
- [Восстановление леса AD. обнаружение проблемы](AD-Forest-Recovery-Identify-the-Problem.md)
- [Восстановление леса AD. Определение способа восстановления](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [Восстановление леса AD — выполнение начального восстановления](AD-Forest-Recovery-Perform-initial-recovery.md)
- [Восстановление леса AD — процедуры](AD-Forest-Recovery-Procedures.md)
- [Восстановление леса AD — часто задаваемые вопросы](AD-Forest-Recovery-FAQ.md)
- [Восстановление леса Active Directory. Восстановление одного домена в лесу с несколькими доменами](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)
- [Восстановление леса Active Directory — восстановление леса с контроллерами домена Windows Server 2003](AD-Forest-Recovery-Windows-Server-2003.md)
