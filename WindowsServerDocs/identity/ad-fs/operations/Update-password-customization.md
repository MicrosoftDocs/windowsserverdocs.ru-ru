---
ms.assetid: 7e804590-6d6c-4cca-ac14-02d4dff06cec
title: Изменение настройки пароля
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cb5fd0ff432e441900e379d3fe798dbe6aef855f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816107"
---
# <a name="update-password-customization"></a>Изменение настройки пароля 


Возможны ситуации, когда пользователи не смогут подключиться к корпоративной сети, чтобы изменить пароль к своей учетной записи. Это может создавать проблемы, особенно для удаленных сотрудников, которые зачастую живут далеко от ближайшего офиса компании. Для подобных особых случаев страница обновления паролей может использоваться только при наличии подключения к Интернету.  
  
Можно настроить страницу обновления пароля, предоставив собственное описание страницы.  
  
> Для включения страницы обновления паролей перейдите в раздел "Управление AD FS" в области "Конечные точки". Конечная точка для обновления пароля расположена внизу, под заголовком "Прочие" — /adfs/portal/updatepassword/. Включив конечную точку, необходимо перезапустить службу AD FS. Это делается вручную. Затем можно перейти по ссылке https://<fqdn>/adfs/portal/updatepassword/ с присоединенного к рабочему месту устройства, отобразится страница обновления пароля.  
  
![update](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)  
  
## <a name="customize-the-update-password-page-description"></a>Настройка описания страницы обновления пароля  
Чтобы настроить описание страницы обновления пароля, используйте следующий командлет и синтаксис Windows PowerShell.  
  

    Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."  

## <a name="additional-references"></a>Дополнительная справка 
[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)  
