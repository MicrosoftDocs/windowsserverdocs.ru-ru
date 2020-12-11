---
description: Дополнительные сведения о развертывании AD DS в Организации Windows Server 2003
ms.assetid: e6b72a80-e8b7-4305-be0c-0a290f468d36
title: Развертывание доменных служб Active Directory в организации Windows Server 2003
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 4aef979fe6dc3fc59bcfb3d6e97da943ee6b2187
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97047082"
---
# <a name="deploying-ad-ds-in-a-windows-server-2003-organization"></a>Развертывание доменных служб Active Directory в организации Windows Server 2003

> Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Если ваша организация в настоящее время работает под управлением Windows Server 2003 Active Directory, можно развернуть Windows Server 2008 домен Active Directory Services (AD DS), выполнив обновление на месте некоторых или всех операционных систем контроллеров домена до Windows Server 2008 или путем введения контроллеров домена под управлением Windows Server 2008 в вашу среду.

Перед добавлением контроллера домена под управлением Windows Server 2008 в существующий домен Active Directory Windows Server 2003 необходимо запустить средство **adprep**, запускаемое из командной строки. Adprep расширяет схему AD DS, обновляет дескрипторы безопасности по умолчанию для выбранных объектов и добавляет новые объекты каталога в соответствии с требованиями некоторых приложений. Средство Adprep доступно на установочном диске Windows Server 2008 (\sources\adprep\adprep.exe). Дополнительные сведения см. в разделе [adprep](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731728(v=ws.11)).

На следующем рисунке показаны шаги для развертывания Windows Server 2008 AD DS в сетевой среде, в которой в настоящее время работает Windows Server 2003 Active Directory.

![развертывание в Организации Windows 2003](media/Deploying-AD-DS-in-a-Windows-Server-2003-Organization/900c4eee-1119-4a9a-9310-755597428b71.gif)

> [!NOTE]
> Если вы хотите задать функциональный уровень домена или леса для Windows Server 2008, все контроллеры домена в среде должны работать под управлением операционной системы Windows Server 2008.

Консолидация доменов ресурсов и доменов учетных записей, которые были обновлены на месте, из среды Windows Server 2003 в составе развертывания AD DS Windows Server 2008 может потребовать реструктуризации домена в пределах леса или леса. Реструктуризация AD DS доменов между лесами помогает сократить сложность представления Организации в AD DS и помогает снизить связанные административные затраты. Реструктуризация AD DS доменов в пределах леса помогает уменьшить административные расходы на организацию за счет сокращения трафика репликации, уменьшения необходимого количества пользователей и групп, а также упрощения администрирования групповая политика. Дополнительные сведения см. в статье [руководство по ADMT: миграция и реструктуризация Active Directory доменов](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc974332(v=ws.10)).

Список подробных задач, которые можно использовать для планирования и развертывания AD DS в Организации, работающей под Windows Server 2003 Active Directory, см. [в разделе Контрольный список: развертывание AD DS в Организации Windows server 2003](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc771407(v=ws.10)).
