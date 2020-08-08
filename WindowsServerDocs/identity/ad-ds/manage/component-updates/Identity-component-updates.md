---
ms.assetid: 7e87ce2b-062e-479f-bcf2-585b6c42026a
title: Обновление компонентов удостоверений
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 419a51800670db24bc77cae5ef1b11ed6090e055
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972311"
---
# <a name="identity-component-updates"></a>Обновление компонентов удостоверений

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="lesson-1-identity-component-updates"></a>Занятие 1. обновления компонента удостоверений
На этом занятии объясняются обновления компонента удостоверений в Windows Server 2012 R2.

### <a name="what-you-will-learn"></a>Обзор учебника
После завершения этого занятия вы сможете:

-   Опишите следующие изменения:

    -   [Уникальность имен субъектов-служб и участников-пользователей](../../../ad-ds/manage/component-updates/SPN-and-UPN-uniqueness.md)

    -   [Вход автоматического перезапуска Winlogon &#40;АРСО&#41;](../../../ad-ds/manage/component-updates/Winlogon-Automatic-Restart-Sign-On--ARSO-.md)

    -   [Аттестация ключей доверенного платформенного модуля (TPM Key) Attestation](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md)

    -   [Командлеты Windows PowerShell для резервного копирования и восстановления ЦС](../../../ad-ds/manage/component-updates/CA-Backup-and-Restore-Windows-PowerShell-cmdlets.md)

    -   [Аудит процессов командной строки](../../../ad-ds/manage/component-updates/Command-line-process-auditing.md)

    -   [Защита учетных данных и управление ими](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn408190(v=ws.11))

**Автор**: Джастин Тернер, старший инженер по расширению поддержки с группой Windows

> [!NOTE]
> Этот материал создан инженером службы поддержки клиентов Майкрософт и предназначен для опытных администраторов и архитекторов систем, которым нужны более глубокие технические сведения о функциях и решениях в Windows Server 2012 R2, а не обычная информация, доступная в статьях на сайте TechNet. Однако он не был отредактирован согласно требованиям сайта, поэтому некоторые формулировки могут быть не такими выверенными, как на станицах TechNet.

