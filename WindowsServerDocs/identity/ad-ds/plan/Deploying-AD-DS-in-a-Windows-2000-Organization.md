---
ms.assetid: 7530cafe-98d7-46c9-95d9-e49d39caa021
title: Развертывание доменных служб Active Directory в организации Windows 2000
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 0a7dea03934a085961a8662f77b2c041b3040e17
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624312"
---
# <a name="deploying-ad-ds-in-a-windows-2000-organization"></a>Развертывание доменных служб Active Directory в организации Windows 2000

> Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Если ваша организация в настоящее время работает под управлением Windows 2000 Active Directory, можно развернуть Windows Server 2008 домен Active Directory Services (AD DS), выполнив обновление на месте некоторых или всех операционных систем контроллеров домена до Windows Server 2008 или поместив контроллеры домена под управлением Windows Server 2008 в вашу среду.

Перед добавлением контроллера домена под управлением Windows Server 2008 в существующий домен Active Directory Windows 2000 необходимо запустить программу **adprep**, программу командной строки. Adprep расширяет схему AD DS, обновляет дескрипторы безопасности по умолчанию для выбранных объектов и добавляет новые объекты каталога в соответствии с требованиями некоторых приложений. Средство Adprep доступно на установочном диске Windows Server 2008 (\саурцес\адпреп\адпреп.ЕКСЕ). Дополнительные сведения см. в разделе [adprep](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731728(v=ws.11)).

> [!NOTE]
> Если вы хотите выполнить обновление на месте существующего контроллера домена Windows 2000 AD DS до Windows Server 2008, необходимо сначала обновить сервер до Windows Server 2003, а затем обновить его до Windows Server 2008.

На следующем рисунке показаны шаги для развертывания AD DS Windows Server 2008 в сетевой среде, в которой в настоящее время работает Active Directory Windows 2000.

![развертывание в Организации Windows 2000](media/Deploying-AD-DS-in-a-Windows-2000-Organization/ee51218a-a858-49d9-8b99-9986679191c1.gif)

> [!NOTE]
> Если вы хотите задать функциональный уровень домена или леса для Windows Server 2008, все контроллеры домена в среде должны работать под управлением операционной системы Windows Server 2008.

Консолидация ресурсов и доменов учетных записей, которые были обновлены в среде Windows 2000 в составе развертывания AD DS Windows Server 2008, может потребовать реструктуризации домена в пределах леса или леса. Реструктуризация AD DS доменов между лесами помогает сократить сложность организации и связанные с ней административные расходы. Реструктуризация AD DS доменов в лесу позволяет снизить административные издержки на организацию за счет сокращения трафика репликации, уменьшения объема необходимого администрирования пользователей и групп, а также упрощения администрирования групповая политика. Дополнительные сведения см. в статье [руководство по ADMT: миграция и реструктуризация Active Directory доменов](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc974332(v=ws.10)).

Список подробных задач, которые можно использовать для планирования и развертывания AD DS в Организации, на которой в настоящее время работает Active Directory Windows 2000, см. [в разделе Контрольный список: развертывание AD DS в Организации windows 2000](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732737(v=ws.10)).
