---
description: Дополнительные сведения см. в статье Оценка стратегии развертывания AD DS
ms.assetid: 4f835b82-67b9-428c-b634-ce133cca5113
title: Оценка примеров стратегии развертывания доменных служб Active Directory
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 5612bc24e3f0662103aae1d831578c7417cc578e
ms.sourcegitcommit: d2224cf55c5d4a653c18908da4becf94fb01819e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2020
ms.locfileid: "97711799"
---
# <a name="evaluating-ad-ds-deployment-strategy-examples"></a>Оценка примеров стратегии развертывания доменных служб Active Directory

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Рассмотрим следующий пример вымышленной компании Contoso Pharmaceuticals, которая развертывает службы домен Active Directory Services (AD DS) в своей среде. Среда Contoso состоит из четырех доменов. Функциональный уровень леса — Windows Server 2003. На следующем рисунке показана текущая структура домена для компании Contoso.

![Иллюстрация, показывающая текущую структуру доменов для компании Contoso.](media/Evaluating-AD-DS-Deployment-Strategy-Examples/3dd79e00-48f8-4927-989c-c55a79caf1be.gif)

После проверки существующей среды и определения целей развертывания компания Contoso установила следующую стратегию развертывания AD DS:

-   Обновите домены Windows Server 2003 до доменов Windows Server 2008.

-   Включение расширенных функций AD DS путем повышения функциональных уровней домена и леса до Windows Server 2008.

-   Измените структуру домена africa.concorp.contoso.com в лесу, чтобы консолидировать этот домен с доменом EMEA. Corp. contoso. Con.

Повышение функционального уровня леса до Windows Server 2008 позволит компании Contoso воспользоваться всеми преимуществами новых функций AD DS. При реструктуризации доменов в пределах леса, как показано на следующем рисунке, уменьшается объем администрирования, необходимый для управления доменами.

![Стратегия развертывания AD DS](media/Evaluating-AD-DS-Deployment-Strategy-Examples/1c061755-413d-452d-b121-6910f8555327.gif)



