---
title: Однократный выход для OpenID Connect в AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/17/2017
ms.topic: article
ms.openlocfilehash: 1ab6735e09d912bac5b1a319a3793ee6e0c70fa2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964941"
---
#  <a name="single-log-out-for-openid-connect-with-ad-fs"></a>Однократный выход для OpenID Connect в AD FS

## <a name="overview"></a>Обзор
Основываясь на начальной поддержке OAuth в AD FS в Windows Server 2012 R2, AD FS 2016 представил поддержку входа OpenID Connect Connect. С помощью [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)AD FS 2016 теперь поддерживает единый выход для сценариев OpenID Connect Connect. В этой статье приводится обзор сценария единого выхода для OpenID Connect Connect и приведены рекомендации по его использованию для приложений OpenID Connect Connect в AD FS.


## <a name="discovery-doc"></a>Документ обнаружения
OpenID Connect Connect использует документ JSON, называемый "документом обнаружения", чтобы предоставить сведения о конфигурации.  Сюда входят URI проверки подлинности, токена, userInfo и общедоступных конечных точек.  Ниже приведен пример документа Discovery.

```
{
"issuer":"https://fs.fabidentity.com/adfs",
"authorization_endpoint":"https://fs.fabidentity.com/adfs/oauth2/authorize/",
"token_endpoint":"https://fs.fabidentity.com/adfs/oauth2/token/",
"jwks_uri":"https://fs.fabidentity.com/adfs/discovery/keys",
"token_endpoint_auth_methods_supported":["client_secret_post","client_secret_basic","private_key_jwt","windows_client_authentication"],
"response_types_supported":["code","id_token","code id_token","id_token token","code token","code id_token token"],
"response_modes_supported":["query","fragment","form_post"],
"grant_types_supported":["authorization_code","refresh_token","client_credentials","urn:ietf:params:oauth:grant-type:jwt-bearer","implicit","password","srv_challenge"],
"subject_types_supported":["pairwise"],
"scopes_supported":["allatclaims","email","user_impersonation","logon_cert","aza","profile","vpn_cert","winhello_cert","openid"],
"id_token_signing_alg_values_supported":["RS256"],
"token_endpoint_auth_signing_alg_values_supported":["RS256"],
"access_token_issuer":"http://fs.fabidentity.com/adfs/services/trust",
"claims_supported":["aud","iss","iat","exp","auth_time","nonce","at_hash","c_hash","sub","upn","unique_name","pwd_url","pwd_exp","sid"],
"microsoft_multi_refresh_token":true,
"userinfo_endpoint":"https://fs.fabidentity.com/adfs/userinfo",
"capabilities":[],
"end_session_endpoint":"https://fs.fabidentity.com/adfs/oauth2/logout",
"as_access_token_token_binding_supported":true,
"as_refresh_token_token_binding_supported":true,
"resource_access_token_token_binding_supported":true,
"op_id_token_token_binding_supported":true,
"rp_id_token_token_binding_supported":true,
"frontchannel_logout_supported":true,
"frontchannel_logout_session_supported":true
}

```



Следующие дополнительные значения будут доступны в документе обнаружения для указания поддержки выхода из внешнего канала:

- frontchannel_logout_supported: значение будет равно "true"
- frontchannel_logout_session_supported: значение будет равно "true".
- end_session_endpoint: это URI выхода OAuth, который клиент может использовать для инициации выхода на сервер.


## <a name="ad-fs-server-configuration"></a>Конфигурация сервера AD FS
Свойство AD FS Енаблеоауслогаут будет включено по умолчанию.  Это свойство указывает серверу AD FS на поиск URL-адреса (Логаутури) с ИД безопасности для инициации выхода на клиент.
Если вы не установили [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) , можно использовать следующую команду PowerShell:

```PowerShell
Set-ADFSProperties -EnableOAuthLogout $true
```

>[!NOTE]
> `EnableOAuthLogout`После установки [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)параметр будет помечен как устаревший. `EnableOAUthLogout`всегда будет иметь значение true и не повлияет на функциональность выхода.

>[!NOTE]
>frontchannel_logout поддерживается **только** после сбой установки [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)

## <a name="client-configuration"></a>Настройка клиента
Клиенту необходимо реализовать URL-адрес, который выполнит вход вошедшего в систему пользователя. Администратор может настроить Логаутури в конфигурации клиента с помощью следующих командлетов PowerShell.


- `(Add | Set)-AdfsNativeApplication`
- `(Add | Set)-AdfsServerApplication`
- `(Add | Set)-AdfsClient`

```PowerShell
Set-AdfsClient -LogoutUri <url>
```

`LogoutUri`— Это URL-адрес, используемый AF FS для выхода пользователя из системы. `LogoutUri`Чтобы реализовать, клиенту необходимо убедиться, что он очищает состояние проверки подлинности пользователя в приложении, например, удаляя маркеры проверки подлинности, которые он содержит. AD FS будет просматривать этот URL-адрес с идентификатором SID в качестве параметра запроса, который сообщает проверяющей стороне или приложению о необходимости выхода пользователя из системы.

![Пользовательская схема выхода ADFS](media/ad-fs-logout-openid-connect/adfs_single_logout2.png)

1.  **Токен OAuth с идентификатором сеанса**: AD FS включает идентификатор сеанса в маркере OAuth во время выдачи маркера id_token. Он будет использоваться позже AD FS для идентификации файлов cookie единого входа, которые будут очищены для пользователя.
2.  **Пользователь инициирует выход**из приложения App1: пользователь может инициировать выход из любого из приложений, вошедших в систему. В этом примере сценария пользователь инициирует выход из App1.
3.  **Приложение отправляет запрос на выход в AD FS**: после того, как пользователь инициирует выход, приложение ОТПРАВЛЯЕТ запрос GET для end_session_endpoint AD FS. Приложение может дополнительно включать id_token_hint в качестве параметра для этого запроса. Если id_token_hint имеется, AD FS будет использовать его вместе с ИДЕНТИФИКАТОРом сеанса, чтобы определить, какой URI следует перенаправить клиенту после выхода из системы (post_logout_redirect_uri).  Post_logout_redirect_uri должен быть допустимым URI, зарегистрированным в AD FS с помощью параметра Редиректурис.
4.  **AD FS отправляет вход клиентам, вошедшим в систему**. AD FS использует значение идентификатора сеанса для поиска соответствующих клиентов, в которые входит пользователь. Идентифицированные клиенты отправляют запрос на Логаутури, зарегистрированный в AD FS, чтобы инициировать выход на стороне клиента.

## <a name="faqs"></a>Часто задаваемые вопросы
**Вопрос.** В документе Discovery не отображаются параметры frontchannel_logout_supported и frontchannel_logout_session_supported.</br>
Ответ **.** Убедитесь, что на всех AD FS серверах установлен [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) . См. один выход на сервер 2016 с [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801).

**Вопрос.** Я настроил единый выход как наименее, но пользователь продолжает входить на другие клиенты.</br>
Ответ **.** Убедитесь, что `LogoutUri` задано значение для всех клиентов, на которых пользователь вошел в систему. Кроме того, AD FS выполняет наилучшую попытку отправки запроса на выход на зарегистрированный `LogoutUri` . Клиент должен реализовать логику для обработки запроса и предпринимать действия для выхода пользователя из приложения.</br>

**Вопрос.** Если после выхода из системы один из клиентов вернется к AD FS с действительным маркером обновления, будет ли AD FS выдавать маркер доступа?</br>
**Ответ.** Да. Клиентское приложение отвечает за удаление всех прошедших проверку артефактов после получения запроса на выход `LogoutUri` .


## <a name="next-steps"></a>Next Steps
[Разработка AD FS](../../ad-fs/AD-FS-Development.md)
