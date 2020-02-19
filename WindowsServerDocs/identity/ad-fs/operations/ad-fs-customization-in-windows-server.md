---
ms.assetid: 25f5aff1-6abf-4dea-b531-f1d9943bc181
title: Настройка AD FS в Windows Server 2016
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: f7402cf549a7a2fb4b112bf92b36182f882b9d73
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465248"
---
# <a name="ad-fs-customization-in-windows-server-2016"></a>Настройка AD FS в Windows Server 2016


В ответ на отзывы от организаций, использующих AD FS, мы добавили дополнительные средства для настройки пользовательского интерфейса входа для отдельных приложений, защищенных AD FS.  
Помимо указания веб-содержимого для каждого приложения, например текста описания и ссылок, теперь можно указать все веб-темы для каждого приложения.  Сюда входят логотип, иллюстрация, таблицы стилей или весь файл OnLoad. js.  
  
## <a name="global-settings"></a>Глобальные параметры    
Общие глобальные параметры можно найти в статье [настройка AD FS страниц входа](https://technet.microsoft.com/library/dn280950.aspx) в систему, поставляемых с AD FS в Windows Server 2012 R2.  
  
## <a name="pre-requisites"></a>Предварительные требования  
Перед выполнением процедур, описанных в этом документе, необходимо выполнить следующие предварительные требования.  
  
-   AD FS в Windows Server 2016 TP4; или более поздней версии  
  
## <a name="configure-ad-fs-relying-parties"></a>Настройка проверяющих сторон AD FS  
Веб-элементы и темы для входа на проверяющую сторону можно настроить с помощью примеров PowerShell, приведенных ниже.  
  
### <a name="customize-messages"></a>Настройка сообщений  
  
```  
PS C:\>Set-AdfsRelyingPartyWebContent  
    -TargetRelyingPartyName "<RP trust Name>"  
    -CompanyName "This text appears in place of the federation service display name"  
    -OrganizationalNameDescriptionText "This text appears right below the company name"  
    -SignInPageDescription "This text appears below the credential prompt"  
```  
  
### <a name="customize-company-name-logo-and-image"></a>Настройка имени компании, логотипа и изображения  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -Logo @{path="C:\Images\applogo.png"}  
    -Illustration @{path="C:\Images\appillustration.jpg"}  
```  
  
### <a name="customize-entire-page"></a>Настроить всю страницу  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -OnLoadScriptPath @{path="c:\scripts\adfstheme\onload.js"}  
```  
  
## <a name="custom-themes-and-advanced-custom-themes"></a>Пользовательские темы и дополнительные пользовательские темы  
  
Сведения о пользовательских темах см. в разделе [Настройка страниц входа AD FS](https://technet.microsoft.com/library/dn280950.aspx) и [расширенная настройка AD FS страниц входа.](https://technet.microsoft.com/library/dn636121.aspx)  
  
## <a name="assigning-custom-web-themes-per-rp"></a>Назначение пользовательских веб-тем для RP  
  
Чтобы назначить пользовательскую тему на RP, используйте следующую процедуру:  
  
1. Создать новую тему как копию для глобальной темы по умолчанию в AD FS  
`New-AdfsWebTheme -Name AppSpecificTheme -SourceName default`  
2. Экспорт темы для настройки  
`Export-AdfsWebTheme -Name AppSpecificTheme -DirectoryPath c:\appspecifictheme`  
3. Настройка файлов тем (изображений, CSS, OnLoad. js) — в любом любимом редакторе или при замене файла  
4. Импорт настроенных файлов из файловой системы в AD FS (для новой темы)  
`Set-AdfsWebTheme -TargetName AppSpecificTheme -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';Path="c:\appspecifictheme\script\onload.js"}`  
5. Применить новую настроенную тему к конкретному RP (или RP)  
`Set-AdfsRelyingPartyWebTheme -TargetRelyingPartyName urn:app1 -SourceWebThemeName AppSpecificTheme`  
  
## <a name="home-realm-discovery"></a>Обнаружение домашней области  
Сведения о настройке обнаружения домашней области см. [в разделе Настройка страниц входа AD FS](https://technet.microsoft.com/library/dn280950.aspx).  
  
## <a name="updated-password-page"></a>Страница обновленного пароля  
Сведения о настройке страницы "Обновление пароля" см. [в разделе Настройка страниц входа AD FS](https://technet.microsoft.com/library/dn280950.aspx).  
  
## <a name="customizing-and-alternate-ids"></a>Настройка и альтернативные идентификаторы  
Пользователи могут входить в приложения с поддержкой службы федерации Active Directory (AD FS) (AD FS), используя любую форму идентификатора пользователя, принимаемого службами домен Active Directory (AD DS). К ним относятся имена участников-пользователей (UPN) (johndoe@contoso.com) или полные доменные имена учетных записей SAM (contoso\johndoe или contoso. ком\жохндое).  Дополнительные сведения об этом см. в разделе [Настройка альтернативного имени пользователя.](Configuring-Alternate-Login-ID.md)  
  
Кроме того, вы можете настроить страницу входа AD FS, чтобы дать конечным пользователям указание о альтернативном ИДЕНТИФИКАТОРе входа. Для этого можно добавить настраиваемое описание страницы входа. Дополнительные сведения см [. в разделе Настройка страниц входа AD FS.](https://technet.microsoft.com/library/dn280950.aspx)   
  
Это можно также сделать, настроив строку "вход с помощью учетной записи организации" над полем username (имя пользователя).  Дополнительные сведения см. в разделе [Расширенная настройка AD FS страниц входа](https://technet.microsoft.com/library/dn636121.aspx).  

## <a name="additional-references"></a>Дополнительная справка 
[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)  
