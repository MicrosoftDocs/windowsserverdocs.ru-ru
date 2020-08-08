---
title: Подготовка к миграции прокси-сервера федерации AD FS 2.0
description: Содержит сведения о готовности к переносу прокси-сервера AD FS Server в Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: e0a040dd3ec717e1315c842d6e6b407025ceabfd
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940665"
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-proxy"></a>Подготовка к миграции прокси-сервера федерации AD FS 2.0

Чтобы подготовиться к переносу прокси-сервера AD FS 2,0 Федерации на Windows Server 2012, необходимо экспортировать и создать резервную копию данных конфигурации AD FS с помощью этого прокси-сервера.  Действия, описанные в этом разделе, относятся к сценарию с одним или несколькими прокси-серверами федерации.

 Чтобы экспортировать данные конфигурации AD FS, выполните следующие действия.

-   [Шаг 1. Экспорт параметров службы прокси-сервера](#step-1-export-proxy-service-settings)

-   [Шаг 2. Резервное копирование пользовательских настроек веб-страницы](#step-2-back-up-webpage-customizations)

##  <a name="step-1-export-proxy-service-settings"></a>Шаг 1. Экспорт параметров службы прокси-сервера
 Чтобы экспортировать параметры службы прокси-сервера федерации, выполните следующие действия.

### <a name="to-export-proxy-service-settings"></a>Экспорт параметров службы прокси-сервера

1.  Экспортируйте SSL-сертификат и его закрытый ключ в PFX-файл. Дополнительные сведения см. в разделе [Export the Private Key Portion of a Server Authentication Certificate](export-the-private-key-portion-of-a-server-authentication-certificate.md).

> [!NOTE]
>  Этот шаг не является обязательным, потому что этот сертификат сохраняется во время обновления операционной системы.

2. Экспортируйте свойства прокси-сервера федерации AD FS 2.0 в файл. Это можно сделать с помощью Windows PowerShell.

Откройте Windows PowerShell и выполните следующую команду, чтобы добавить командлеты AD FS в сеанс Windows PowerShell: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Затем выполните следующую команду для экспорта свойств прокси-сервера федерации в файл: `PSH:> Get-ADFSProxyProperties | out-file “.\proxyproperties.txt”`.

3. Убедитесь, что вам известны данные учетной записи администратора сервера федерации AD FS или учетной записи службы, от имени которой выполняется служба федерации AD FS.  Эти сведения необходимы для настройки доверия прокси-сервера.

   При выполнении этого шага осуществляется сбор следующих сведений, необходимых для настройки прокси-сервера федерации AD FS:

-   имя службы федерации AD FS;

-   имя учетной записи домена, которая необходима для настройки доверия прокси-сервера;

-   адрес и порт прокси-сервера HTTP (если между прокси-сервером федерации AD FS и серверами федерации AD FS есть прокси-сервер HTTP).

##  <a name="step-2-back-up-webpage-customizations"></a>Шаг 2. Резервное копирование пользовательских настроек веб-страницы
 Чтобы выполнить резервное копирование пользовательских настроек веб-страницы, скопируйте веб-страницы прокси-сервера AD FS и файл **web.config** из каталога, сопоставленного виртуальному пути **“/adfs/ls”** , в IIS.  По умолчанию он находится в каталоге **%systemdrive%\inetpub\adfs\ls**.

## <a name="next-steps"></a>Next Steps
 [Подготовка к переносу сервера федерации AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md) [Подготовка к переносу AD FS 2,0 прокси-](prepare-to-migrate-ad-fs-fed-proxy.md) сервер федерации миграция [сервера AD FS 2,0 сервер федерации](migrate-the-ad-fs-fed-server.md) миграция [AD FS 2,0 прокси-сервер](migrate-the-ad-fs-2-fed-server-proxy.md) [AD FS 1,1](migrate-the-ad-fs-web-agent.md)