---
ms.assetid: f7002265-60fa-40b8-9dd7-4bf131d9320a
title: Именование компьютеров
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 37f877b3165f5de31c8a26ae4000b8064362fa17
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947852"
---
# <a name="computer-naming"></a>Именование компьютеров

> Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Когда компьютер под управлением операционной системы Windows 2000, Windows XP, Windows Server 2003, Windows Server 2008 или Windows Vista присоединяется к домену, по умолчанию компьютеру присваивается имя. Имя, присваиваемое ему, состоит из имени узла компьютера (то есть имени компьютера в свойствах системы) и имени службы доменных имен (DNS) Active Directory домена, к которому присоединен компьютер (то есть первичный DNS-суффикс в свойствах системы). Объединение имени узла и DNS-имени домена называется полным доменным именем (FQDN). Например, если компьютер с именем узла Server1 присоединяется к домену corp.contoso.com, полное доменное имя компьютера — server1.corp.contoso.com.

Если у компьютера уже есть другое доменное имя DNS, которое было статически указано в зоне DNS или зарегистрировано в интегрированной службе DHCP-сервера, полное доменное имя компьютера отличается от имени, которое было зарегистрировано ранее. На компьютер может ссылаться любое имя.

Дополнительные сведения о соглашениях об именовании в домен Active Directory Services (AD DS) см. [в разделе соглашения об именовании в Active Directory для компьютеров, доменов, сайтов и подразделений](https://support.microsoft.com/help/909264/).
