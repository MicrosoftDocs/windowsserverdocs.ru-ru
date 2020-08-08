---
ms.assetid: 7e804590-6d6c-4cca-ac14-02d4dff06cec
title: Изменение настройки пароля
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: c47649e5a60de646de331a6c723c18c3b041bca6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967011"
---
# <a name="update-password-customization"></a>Изменение настройки пароля

Возможны ситуации, когда пользователи не смогут подключиться к корпоративной сети, чтобы изменить пароль к своей учетной записи. Это может создавать проблемы, особенно для удаленных сотрудников, которые зачастую живут далеко от ближайшего офиса компании. Для подобных особых случаев страница обновления паролей может использоваться только при наличии подключения к Интернету.

Можно настроить страницу обновления пароля, предоставив собственное описание страницы.

Для включения страницы обновления паролей перейдите в раздел "Управление AD FS" в области "Конечные точки". Конечная точка для обновления пароля расположена внизу, под заголовком "Прочие" — /adfs/portal/updatepassword/. Включив конечную точку, необходимо перезапустить службу AD FS. Это делается вручную. Если вы предполагаете использовать внешнюю веб-страницу с паролем для обновления, а при использовании прокси приложения — в том же режиме, его необходимо включить на прокси-сервере (включить на прокси-сервере). Затем можно переходить к `https://<fqdn>/adfs/portal/updatepassword/` на устройстве, присоединенном к рабочей области, и вы увидите страницу Обновление пароля.

![обновить](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)

## <a name="customize-the-update-password-page-description"></a>Настройка описания страницы обновления пароля

Чтобы настроить описание страницы обновления пароля, используйте следующий командлет и синтаксис Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."
```

## <a name="additional-references"></a>Дополнительная справка

[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
