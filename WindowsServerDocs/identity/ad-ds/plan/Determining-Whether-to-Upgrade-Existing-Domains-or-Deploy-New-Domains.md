---
description: 'Дополнительные сведения: определение необходимости обновления существующих доменов или развертывание новых доменов'
ms.assetid: c20231dd-2b83-4494-9385-1172272e00d6
title: Обновление имеющихся доменов и развертывание новых доменов
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: b89ea1c898fc1c7a6859b88d2b7ba21d47516d06
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97044072"
---
# <a name="determining-whether-to-upgrade-existing-domains-or-deploy-new-domains"></a>Обновление имеющихся доменов и развертывание новых доменов

> Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Каждый домен в вашем проекте будет либо новым доменом, либо существующим обновленным доменом. Пользователи из существующих доменов, которые не обновляются, должны быть перемещены в новые домены.

Перемещение учетных записей между доменами может повлиять на конечных пользователей. Прежде чем принять решение о том, следует ли переместить пользователей в новый домен или обновить существующие домены, оцените долгосрочные преимущества администрирования нового домена AD DS в отношении стоимости перемещения пользователей в домен.

Дополнительные сведения об обновлении доменов Active Directory до Windows Server 2008 см. в разделе [обновление доменов Active Directory до Windows server 2008 и Windows server 2008 R2 AD DS Domains](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731188(v=ws.10)).

Дополнительные сведения о реструктуризации AD DS доменов в лесах и между лесами см. в разделе [руководство по ADMT: миграция и реструктуризация Active Directory доменов](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc974332(v=ws.10)).

Чтобы получить помощь в документировании планов для новых и обновленных доменов, скачайте Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip из [вспомогательных средств для пакета развертывания Windows Server 2003](https://microsoft.com/download/details.aspx?id=9608) и откройте «планирование домена» (DSSLOGI_5.doc).
