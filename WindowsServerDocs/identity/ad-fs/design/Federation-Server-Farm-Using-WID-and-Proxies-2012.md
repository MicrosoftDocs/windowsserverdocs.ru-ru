---
description: 'Дополнительные сведения: ферма серверов федерации с использованием WID и прокси-серверов'
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: Ферма серверов AD FS Федерации с использованием WID и прокси-серверов
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 673aeabc3cb390e3001880f0a4174291d8b84871
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97046932"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>Ферма серверов федерации с использованием WID и прокси-серверов

Эта топология развертывания для службы федерации Active Directory (AD FS) \( AD FS \) идентична ферме серверов федерации с \( топологией топологии внутренней базы данных WID Windows \) , но добавляет прокси-серверы федерации в сеть периметра для поддержки внешних пользователей. Прокси-серверы федерации перенаправляют запросы проверки подлинности клиента, поступающие за пределы корпоративной сети, в ферму серверов федерации.

## <a name="deployment-considerations"></a>Рекомендации по развертыванию
В этом разделе описываются различные вопросы о предполагаемой аудитории, преимуществах и ограничениях, связанных с этой топологией развертывания.

### <a name="who-should-use-this-topology"></a>Кто должен использовать эту топологию?

-   Организации с 100 или меньше настроенных отношений доверия, которым необходимо предоставить как внутренних пользователей, так и внешних пользователей, которые \( вошли на компьютеры, физически расположенные за пределами корпоративной сети, \) с единым входом единого входа \- \( \) для федеративных приложений или служб.

-   Организации, которым необходимо предоставить единый доступ к Microsoft Office 365, для внутренних пользователей и внешних пользователей.

-   Небольшие организации с внешними пользователями и нуждаются в избыточных, масштабируемых службах

### <a name="what-are-the-benefits-of-using-this-topology"></a>Каковы преимущества использования этой топологии?

-   Те же преимущества, что указаны для [фермы серверов федерации с использованием ТОПОЛОГИИ WID](Federation-Server-Farm-Using-WID-2012.md) , а также преимущества предоставления дополнительных возможностей доступа внешним пользователям.

### <a name="what-are-the-limitations-of-using-this-topology"></a>Каковы ограничения использования этой топологии?

-   Те же ограничения, что указаны для [фермы серверов федерации, использующей](Federation-Server-Farm-Using-WID-2012.md) ТОПОЛОГИю WID.

## <a name="server-placement-and-network-layout-recommendations"></a>Рекомендации по размещению и макету сети сервера
Чтобы развернуть эту топологию, помимо добавления двух прокси-серверов федерации, необходимо убедиться, что сеть периметра также может предоставлять доступ к серверу DNS системы доменных имен \( \) и второму узлу балансировки сетевой нагрузки \( \) . Второй узел балансировки сетевой нагрузки должен быть настроен с использованием кластера балансировки сетевой нагрузки, который использует \- IP-адрес кластера, доступного для Интернета, и должен использовать тот же параметр DNS-имени кластера, что и в предыдущем кластере NLB, настроенном в FS.fabrikam.com корпоративной сети \( \) . Прокси-серверы федерации также должны быть настроены на доступ к Интернету \- .

На следующем рисунке показана существующая ферма серверов федерации с топологией WID, описанная выше, и как вымышленная компания Fabrikam, Inc., предоставляет доступ к DNS-серверу периметра, добавляет второй узел балансировки сетевой нагрузки с тем же DNS-именем кластера \( FS.fabrikam.com \) и добавляет \( \) в сеть периметра два посредника fsp1 и fsp2.

![ферма серверов, использующая WID](media/FarmWIDProxies.gif)

Дополнительные сведения о настройке сетевой среды для использования с серверами федерации или прокси-серверами федерации см. в разделе [требования к разрешению имен для серверов федерации](Name-Resolution-Requirements-for-Federation-Servers.md) или [требования к разрешению имен для прокси](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)-серверов федерации.

## <a name="see-also"></a>См. также:
[Руководство по разработке служб федерации Active Directory в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
