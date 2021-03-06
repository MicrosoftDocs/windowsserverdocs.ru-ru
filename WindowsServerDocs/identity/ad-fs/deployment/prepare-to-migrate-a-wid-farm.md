---
title: Подготовка к миграции фермы AD FS 2,0 WID
description: Содержит сведения о готовности к миграции фермы AD FS 2,0 Server WID на Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: 2393e289e6a20d30db2d5523810437b6c5049fe5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940603"
---
# <a name="prepare-to-migrate-an-ad-fs-20-wid-farm"></a>Подготовка к миграции фермы AD FS 2,0 WID
 Чтобы подготовиться к миграции серверов федерации AD FS 2,0, принадлежащих ферме на основе внутренней базы данных Windows (WID), на Windows Server 2012, необходимо экспортировать и создать резервную копию данных конфигурации AD FS этих серверов.

 Чтобы экспортировать данные конфигурации AD FS, выполните следующие действия.

-   [Шаг 1. Экспорт параметров службы](#step-1-export-service-settings)

-   [Шаг 2. Резервное копирование хранилищ настраиваемых атрибутов](#step-2-back-up-custom-attribute-stores)

-   [Шаг 3. Резервное копирование пользовательских настроек веб-страницы](#step-3-back-up-webpage-customizations)

## <a name="step-1-export-service-settings"></a>Шаг 1. Экспорт параметров службы
 Для того чтобы экспортировать параметры службы, выполните следующие действия.

### <a name="to-export-service-settings"></a>Экспорт параметров службы

1.  Зафиксируйте имя субъекта сертификата и значение отпечатка сертификата SSL, используемого службой федерации. Чтобы найти SSL-сертификат, откройте консоль управления службы IIS (IIS), выберите **веб-сайт по умолчанию** в левой области, щелкните **привязки...** на панели **Действие** , найдите и выберите HTTPS-привязки, нажмите **Изменить**, а затем — **Просмотр**.

> [!NOTE]
>  Кроме того, можно экспортировать SSL-сертификат и его закрытый ключ в PFX-файл. Дополнительные сведения см. в разделе [Export the Private Key Portion of a Server Authentication Certificate](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md).
>
>  Этот шаг не является обязательным, потому что сертификат хранится в хранилище личных сертификатов на локальном компьютере и сохраняется при обновлении ОС.

2. Помимо самозаверяющих сертификатов нужно экспортировать любые сертификаты подписи токена, шифрования токена или взаимодействия служб и ключи, которые не создаются внутри организации.

С помощью Windows PowerShell можно просмотреть все сертификаты, используемые на сервере. Откройте Windows PowerShell и выполните следующую команду, чтобы добавить командлеты AD FS в сеанс Windows PowerShell: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Затем выполните следующую команду для просмотра всех сертификатов, используемых на сервере `PSH:>Get-ADFSCertificate`. Результат выполнения этой команды содержит значения StoreLocation и StoreName, указывающие на расположение хранилища каждого сертификата.  Затем можно воспользоваться инструкциями в статье [Экспорт части сертификата аутентификации сервера с закрытым ключом](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md), чтобы экспортировать каждый сертификат и его закрытый ключ в PFX-файл.

> [!NOTE]
>  Этот шаг не является обязательным, потому что все внешние сертификаты во время обновления операционной системы сохраняются.

3. Запишите удостоверение учетной записи службы федерации AD FS 2.0 и пароль этой учетной записи.

Чтобы найти значение удостоверения, просмотрите столбец **Вход от имени****службы Windows AD FS 2.0** на консоли **Службы**. Запишите это значение вручную.

## <a name="step-2-back-up-custom-attribute-stores"></a>Шаг 2. Резервное копирование хранилищ настраиваемых атрибутов
 Сведения об используемых в AD FS хранилищах настраиваемых атрибутов можно найти с помощью Windows PowerShell. Откройте Windows PowerShell и выполните следующую команду, чтобы добавить командлеты AD FS в сеанс Windows PowerShell: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Затем выполните следующую команду, чтобы найти сведения о хранилищах настраиваемых атрибутов: `PSH:>Get-ADFSAttributeStore`. Действия по обновлению или переносу пользовательских хранилищ атрибутов могут быть разными.

## <a name="step-3-back-up-webpage-customizations"></a>Шаг 3. Резервное копирование пользовательских настроек веб-страницы
 Чтобы выполнить резервное копирование пользовательских настроек веб-страницы, копируйте веб-страницы AD FS и файл **web.config** из каталога, сопоставленного виртуальному пути **“/adfs/ls”**, в IIS. По умолчанию он находится в каталоге **%systemdrive%\inetpub\adfs\ls**.

## <a name="next-steps"></a>Next Steps
 [Подготовка к переносу сервера федерации AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md) [Подготовка к переносу AD FS 2,0 прокси-](prepare-to-migrate-ad-fs-fed-proxy.md) сервер федерации миграция [сервера AD FS 2,0 сервер федерации](migrate-the-ad-fs-fed-server.md) миграция [AD FS 2,0 прокси-сервер](migrate-the-ad-fs-2-fed-server-proxy.md) [AD FS 1,1](migrate-the-ad-fs-web-agent.md)