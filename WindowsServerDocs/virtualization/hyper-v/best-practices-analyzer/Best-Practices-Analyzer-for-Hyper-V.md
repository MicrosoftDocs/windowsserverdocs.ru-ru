---
title: Анализатор соответствия рекомендациям для Hyper-V
description: Узнайте, как анализатор соответствия рекомендациям сканирует компьютер с помощью правил, основанных на этих рекомендациях, и сообщает о результатах.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 3747faa5-6e9f-499e-8a79-3fb9d73b6b92
ms.date: 8/16/2016
ms.openlocfilehash: a7261e219ffc332cc0ea79fb9c6de6f9e0624b4f
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834499"
---
# <a name="best-practices-analyzer-for-hyper-v"></a>Анализатор соответствия рекомендациям для Hyper-V

> Область применения. Windows Server 2016

*Рекомендации* по управлению Windows — это руководства, которые эксперты считают идеальным способом настройки сервера в обычных условиях. Необязательное возникновение проблем может привести к неоправданным нарушениям рекомендаций. Но они могут указывать на конфигурации серверов, которые могут привести к снижению производительности, снижению надежности, непредвиденным конфликтам, повышению угроз безопасности или другим потенциальным проблемам.

Анализатор соответствия рекомендациям проверяет компьютер с помощью правил, основанных на этих рекомендациях, и сообщает о результатах. Каждое правило рекомендаций содержит сведения о соответствии правила. В этом разделе описываются эти правила, которые помогут вам разобраться с рекомендациями, применяемыми к Hyper-V, а также интерпретировать результаты при обнаружении условий, которые не соответствуют рекомендациям.

Дополнительные сведения о анализатор соответствия рекомендациям и проверках см. в разделе [анализатор соответствия рекомендациям](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283329(v=ws.11)).

## <a name="about-hyper-v"></a>Сведения о Hyper-V
Hyper-V позволяет одновременно запускать несколько операционных систем на одном физическом компьютере, запустив каждую из них на виртуальной машине. Виртуальные машины позволяют более эффективно и гибко использовать вычислительные ресурсы. Дополнительные сведения о Hyper-V см. [в статье Hyper-v на Windows Server 2016](../Hyper-V-on-Windows-Server.md).



