---
ms.assetid: 4f835b82-67b9-428c-b634-ce133cca5113
title: Оценка примеров стратегии развертывания доменных служб Active Directory
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 58236397485e0998e26e9ca67908c7937d32fbbb
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93068636"
---
# <a name="evaluating-ad-ds-deployment-strategy-examples"></a>Оценка примеров стратегии развертывания доменных служб Active Directory

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Рассмотрим следующий пример вымышленной компании Contoso Pharmaceuticals, которая развертывает службы домен Active Directory Services (AD DS) в своей среде. Среда Contoso состоит из четырех доменов. Функциональный уровень леса — Windows Server 2003. На следующем рисунке показана текущая структура домена для компании Contoso.

![Стратегия развертывания AD DS](media/Evaluating-AD-DS-Deployment-Strategy-Examples/3dd79e00-48f8-4927-989c-c55a79caf1be.gif)

После проверки существующей среды и определения целей развертывания компания Contoso установила следующую стратегию развертывания AD DS:

-   Обновите домены Windows Server 2003 до доменов Windows Server 2008.

-   Включение расширенных функций AD DS путем повышения функциональных уровней домена и леса до Windows Server 2008.

-   Измените структуру домена africa.concorp.contoso.com в лесу, чтобы консолидировать этот домен с доменом EMEA. Corp. contoso. Con.

Повышение функционального уровня леса до Windows Server 2008 позволит компании Contoso воспользоваться всеми преимуществами новых функций AD DS. При реструктуризации доменов в пределах леса, как показано на следующем рисунке, уменьшается объем администрирования, необходимый для управления доменами.

![Стратегия развертывания AD DS](media/Evaluating-AD-DS-Deployment-Strategy-Examples/1c061755-413d-452d-b121-6910f8555327.gif)



