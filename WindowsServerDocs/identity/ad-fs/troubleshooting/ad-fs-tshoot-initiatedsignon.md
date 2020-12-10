---
title: AD FS устранение неполадок — Idp-Initiated вход
description: В этом документе описано, как устранить неполадки на странице входа AD FS.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.openlocfilehash: 8ab9497a2c6711c638010c66b9a7c7dd8066876f
ms.sourcegitcommit: 03048411c07c1a1d0c8bb0b2a60c1c17c9987314
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "96938974"
---
# <a name="ad-fs-troubleshooting---idp-initiated-sign-on"></a>AD FS устранение неполадок — Idp-Initiated вход
Страницу входа AD FS можно использовать для проверки работы проверки подлинности.  Это можно сделать, перейдя на страницу и войдя в систему.  Кроме того, можно использовать страницу входа, чтобы убедиться в том, что указаны все проверяющие стороны SAML 2,0.

## <a name="enable-the-idp-initiated-sign-on-page"></a>Включение страницы входа Idp-Initiated
По умолчанию для AD FS в Windows 2016 не включена страница входа.  Чтобы включить его, можно использовать команду PowerShell Set-AdfsProperties.  Для включения страницы используйте следующую процедуру:

1.  Открыть Windows PowerShell
2.  Введите:  `Get-AdfsProperties` и нажмите клавишу ВВОД
3.  Убедитесь, что для **енаблеидпинитиатедсигнонпаже** задано значение false ![ false.](media/ad-fs-tshoot-initiatedsignon/idp2.png)
4.  В PowerShell введите:  `Set-AdfsProperties -EnableIdpInitiatedSignonPage $true`
5.  Вы не увидите подтверждения, поэтому введите Get-AdfsProperties еще раз и убедитесь, что для **енаблеидпинитатедсигнонпаже** задано значение true.
![True](media/ad-fs-tshoot-initiatedsignon/idp4.png)

## <a name="test-authentication"></a>Тест проверки подлинности
Используйте следующую процедуру для проверки подлинности AD FS на странице входа Idp-Initiated.

1.  Откройте веб-браузер и перейдите на страницу входа в IDP.  Пример: https://sts.contoso.com/adfs/ls/idpinitiatedsignon.aspx
2.  Вам будет предложено выполнить вход.  Введите свои учетные данные.
![Вход](media/ad-fs-tshoot-initiatedsignon/idp5.png)
3.  Если это успешно, необходимо войти в.


## <a name="test-authentication-using-a-seamless-logon-experience"></a>Проверка подлинности с помощью простого входа в систему
Вы можете протестировать простой способ входа в систему, убедившись, что URL-адрес для серверов AD FS добавляет зону местной интрасети в свойствах Интернета.  Выполните перечисленные ниже действия.

1.  На клиенте Windows 10 нажмите кнопку Пуск и введите свойства браузера и выберите Свойства обозревателя.
2.   Перейдите на вкладку Безопасность, щелкните Местная интрасеть и нажмите кнопку сайты.
![Общения](media/ad-fs-tshoot-initiatedsignon/idp8.png)
1.  Нажмите кнопку Дополнительно.
2.  Введите URL-адрес и нажмите кнопку Добавить.  Нажмите кнопку Close (Закрыть).
![Добавить URL-адрес](media/ad-fs-tshoot-initiatedsignon/idp9.png)
1.  Нажмите кнопку "ОК".  Нажмите кнопку "ОК".  При этом должны быть закрыты параметры Интернета.
2.  Откройте веб-браузер и перейдите на страницу входа в IDP.  Пример: https://sts.contoso.com/adfs/ls/idpinitiatedsignon.aspx
3.  Нажмите кнопку войти.  Необходимо автоматически войти в систему и не запрашивать учетные данные.
![Общения](media/ad-fs-tshoot-initiatedsignon/idp6.png)

## <a name="next-steps"></a>Next Steps

- [Устранение неполадок в AD FS](ad-fs-tshoot-overview.md)
