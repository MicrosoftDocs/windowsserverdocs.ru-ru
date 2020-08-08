---
title: Обновления компонентов доменных служб Active Directory
description: В этом документе обсуждаются AD DS обновления компонентов для Windows Server 2012 R2
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 09/08/2017
ms.topic: article
ms.assetid: a3a91034-a4da-4ad7-93f8-0cd2ec3e7824
ms.openlocfilehash: 41e696ffd7339269311a9ccf21e096b48ef37439
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943437"
---
# <a name="active-directory-domain-services-component-updates"></a>Обновления компонентов доменных служб Active Directory

>Область применения: Windows Server 2016, Windows Server 2012 R2

В этом модуле содержатся сведения о незначительно обновленных компонентах в области служб каталогов и удостоверений.


| Об авторе |
|------------------|
|   **Автор**    |
|     **Биография**     |
| **Участники** |
|  **Рецензенты**   |

> [!NOTE]
> Этот материал создан инженером службы поддержки клиентов Майкрософт и предназначен для опытных администраторов и архитекторов систем, которым нужны более глубокие технические сведения о функциях и решениях в Windows Server 2012 R2, а не обычная информация, доступная в статьях на сайте TechNet. Однако он не был отредактирован согласно требованиям сайта, поэтому некоторые формулировки могут быть не такими выверенными, как на станицах TechNet.

### <a name="what-you-will-learn"></a>Обзор учебника
После изучения данного модуля вы сможете:

-   объяснять обновления компонентов в области технологий служб каталогов и удостоверений в Windows Server 2012 R2.

    -   [Уникальность имен субъектов-служб и участников-пользователей](../../../ad-ds/manage/component-updates/SPN-and-UPN-uniqueness.md)

    -   [Вход автоматического перезапуска Winlogon &#40;АРСО&#41;](../../../ad-ds/manage/component-updates/Winlogon-Automatic-Restart-Sign-On--ARSO-.md)

    -   [Аттестация ключей доверенного платформенного модуля (TPM Key) Attestation](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md)

    -   [Командлеты Windows PowerShell для резервного копирования и восстановления ЦС](../../../ad-ds/manage/component-updates/CA-Backup-and-Restore-Windows-PowerShell-cmdlets.md)

    -   [Аудит процессов командной строки](../../../ad-ds/manage/component-updates/Command-line-process-auditing.md)

    -   [Защита учетных данных и управление ими](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn408190(v=ws.11))

    -   [Обновления компонентов служб каталогов](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md)

        -   [Режимы работы домена и леса](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)

        -   [Устаревание NTFRS](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)

        -   [Изменения в оптимизаторе запросов LDAP](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)

        -   [Улучшения, связанные с событием 1644](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)

        -   [Повышение пропускной способности репликации Active Directory](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)
