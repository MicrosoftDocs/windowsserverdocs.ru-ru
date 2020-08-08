---
title: Проверка перехода AD FS 2,0 на Windows Server 2012 R2
description: Содержит сведения о миграции AD FS Server на Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.openlocfilehash: 35216baafefc5b304e1fc27b48f99b3afcde32fc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940451"
---
# <a name="verify-the-ad-fs-20-migration-to-windows-server-2012-r2"></a>Проверка перехода AD FS 2,0 на Windows Server 2012 R2

После того как вы выполните ту же миграцию сервера Active Directory служба федерации (AD FS) на Windows Server 2012 R2, можно использовать следующую процедуру, чтобы убедиться в работоспособности серверов федерации в ферме. то есть любой клиент в той же сети может получить доступ к серверам федертатион.

Минимальным требованием для выполнения этой процедуры является членство в одной из следующих групп: **Пользователи**, **Операторы архива**, **Опытные пользователи**, **Администраторы**, — или эквивалентной группе на локальном компьютере.

### <a name="to-verify-that-a-federation-server-is-operational"></a>Проверка работоспособности сервера федерации

1.  Откройте окно браузера и в адресной строке введите имя сервера федерации, а затем добавьте его с помощью, `federationmetadata/2007-06/federationmetadata.xml` чтобы перейти к конечной точке метаданных службы федерации. Например, `https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml` .

Если в окне браузера вы увидите метаданные сервера федерации без каких-либо ошибок или предупреждений по поводу SSL-сертификата, то сервер федерации работоспособен.

2. Также можно перейти на страницу входа служб федерации Active Directory (добавьте к имени службы федерации строку `adfs/ls/idpinitiatedsignon.htm`, например `https://fs.contoso.com/adfs/ls/idpinitiatedsignon.htm`).  Появится страница входа в службы федерации Active Directory, на которой можно выполнить вход с учетными данными администратора домена.

> [!IMPORTANT]
>  Обязательно настройте параметры браузера, чтобы они доверяли роли сервера федерации, добавив имя службы федерации (например, `https://fs.contoso.com` ) в зону локальной интрасети браузера.

## <a name="next-steps"></a>Next Steps
 [Миграция служб ролей службы федерации Active Directory (AD FS) в Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md) [Подготовка к переносу сервера федерации AD FS](prepare-migrate-ad-fs-server-r2.md) [Миграция AD FS сервер федерации](migrate-ad-fs-fed-server-r2.md) , выполняющий миграцию [AD FS прокси-сервера федерации](migrate-fed-server-proxy-r2.md)
