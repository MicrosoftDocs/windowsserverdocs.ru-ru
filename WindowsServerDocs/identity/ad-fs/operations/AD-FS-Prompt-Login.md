---
title: AD FS Prompt = имя входа
description: Часто задаваемые вопросы по AD FS 2016
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.openlocfilehash: 0af0d71ad2b373f755653898ab0697b0308faa4b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940307"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Поддержка параметра prompt=login в службах федерации Active Directory (AD FS)

В следующем документе описывается собственная поддержка параметра Prompt = Login, доступного в AD FS.

## <a name="what-is-promptlogin"></a>Что такое Prompt = имя входа?

Когда приложения должны запрашивать новую проверку подлинности из Azure AD, а это означает, что им требуется Azure AD для повторной проверки подлинности пользователя, даже если пользователь уже прошел проверку подлинности, он может отправить `prompt=login` параметр в Azure AD как часть запроса на проверку подлинности.

Если этот запрос предназначен для федеративного пользователя, Azure AD необходимо сообщить IdP, например AD FS, что запрос предназначен для новой проверки подлинности.

По умолчанию Azure AD преобразуется `prompt=login` в `wfresh=0` и `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` при отправке запросов на проверку подлинности в федеративный IDP.

Эти параметры означают следующее:

- `wfresh=0`: выполнять новую проверку подлинности
- `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`: использовать имя пользователя и пароль для нового запроса проверки подлинности

Это может вызвать проблемы с корпоративными интрасетями и сценариями многофакторной проверки подлинности, в которых требуется тип проверки подлинности, отличный от имени пользователя и пароля, запрошенных `wauth` параметром.

AD FS в Windows Server 2012 R2 с накопительным пакетом обновления за Июль 2016 представил встроенную поддержку для `prompt=login` параметра. Это означает, что теперь Azure AD может отправить этот параметр "как есть" в AD FS службу как часть запросов проверки подлинности Azure AD и Office 365.

## <a name="ad-fs-versions-that-support-promptlogin"></a>AD FS версии, поддерживающие Prompt = имя входа

Ниже приведен список версий AD FS, которые поддерживают `prompt=login` параметр.

- AD FS в Windows Server 2012 R2 с накопительным пакетом обновления за Июль 2016
- AD FS в Windows Server 2016

## <a name="how-to-configure-a-federated-domain-to-send-promptlogin-to-ad-fs"></a>Настройка федеративного домена для отправки запроса = вход в AD FS

Для настройки параметра используйте модуль Azure AD PowerShell.

> [!NOTE]
> `prompt=login`Возможность (включенная `PromptLoginBehavior` свойством) в настоящее время доступна только в [модуле Azure AD PowerShell версии 1,0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185), в котором командлеты имеют имена, включающие "MSOL", например Set-MsolDomainFederationSettings.  В настоящее время он недоступен через версию 2,0 модуля Azure AD PowerShell, у командлетов которых есть такие имена, как Set-AzureAD \* .

1. Сначала получите текущие значения `PreferredAuthenticationProtocol` , `SupportsMfa` и `PromptLoginBehavior` для федеративного домена, выполнив следующую команду PowerShell:

```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | Format-List *
```

> [!NOTE]
> Выходные данные по `Get-MsolDomainFederationSettings` умолчанию не отображают определенные свойства в консоли. Чтобы просмотреть все свойства, необходимо передать `|` его выходные данные, чтобы `Format-List *` принудительно вывести все свойства объекта.

![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)

> [!NOTE]
> Если значение свойства `PromptLoginBehavior` является пустым ( `$null` ), `TranslateToFreshPasswordAuth` используется поведение.

2. Настройте нужное значение `PromptLoginBehavior` , выполнив следующую команду:

```powershell
    Set-MsolDomainFederationSettings –DomainName <your_domain_name> -PreferredAuthenticationProtocol <current_value_from_step1> -SupportsMfa <current_value_from_step1> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

Ниже приведены возможные значения `PromptLoginBehavior` параметра и их значение.

- **Транслатетофрешпассвордаус**: обозначает поведение Azure AD по умолчанию при преобразовании `prompt=login` в `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` и `wfresh=0` .
- **Нативесуппорт**: означает, что `prompt=login` параметр будет отправлен в виде AD FS. Это рекомендуемое значение, если AD FS находится в Windows Server 2012 R2 с накопительным пакетом обновления за Июль 2016 или более поздней версии.
- **Отключено**. означает, что `wfresh=0` отправляется только в AD FS.
