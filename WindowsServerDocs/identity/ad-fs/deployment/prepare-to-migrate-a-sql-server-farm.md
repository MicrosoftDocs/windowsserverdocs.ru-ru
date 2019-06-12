---
title: Подготовка к миграции фермы AD FS SQL
description: Сведения о подготовке к миграции фермы SQL server AD FS в Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3f735c45582bc9d1746f18c0ac7c9888a4b3ac88
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445558"
---
# <a name="prepare-to-migrate-a-sql-server-farm"></a>Подготовка к миграции фермы SQL Server  
 Чтобы подготовиться к миграции серверов AD FS 2.0 federation, относящихся к ферме SQL Server в Windows Server 2012, необходимо экспортировать и резервное копирование данных конфигурации AD FS с этих серверов.  
  
 Чтобы экспортировать данные конфигурации AD FS, выполните следующие действия.  
  
-   [Шаг 1. Экспорт параметров службы](#step-1-export-service-settings)  
  
-   [Шаг 2. Резервное копирование хранилищ настраиваемых атрибутов](#step-2-back-up-custom-attribute-stores)  
  
-   [Шаг 3. Резервное копирование пользовательских настроек веб-страницы](#step-3-back-up-webpage-customizations)  
  
## <a name="step-1-export-service-settings"></a>Шаг 1. Экспорт параметров службы  
 Для того чтобы экспортировать параметры службы, выполните следующие действия.  
  
### <a name="to-export-service-settings"></a>Экспорт параметров службы  
  
1.  Зафиксируйте имя субъекта сертификата и значение отпечатка сертификата SSL, используемого службой федерации. To find the SSL certificate, open the Internet Information Services (IIS) management console, select **Веб-сайт по умолчанию** , щелкните элемент **Привязки…** на панели **Действие** , найдите и выберите HTTPS-привязки, нажмите **Изменить**, а затем — **Просмотр**.  
  
> [!NOTE]
>  Кроме того, можно экспортировать SSL-сертификат и его закрытый ключ в PFX-файл. Дополнительные сведения см. в разделе [Экспорт части закрытого ключа сертификата проверки подлинности сервера](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md).  
>   
>  Этот шаг не является обязательным, потому что сертификат хранится в хранилище личных сертификатов на локальном компьютере и сохраняется при обновлении ОС.  
  
2. Экспортируйте любые другие сертификаты подписи токена, шифрования токена или взаимодействия служб и ключи, которые не создаются внутри организации службами AD FS.  
  
С помощью Windows PowerShell можно просмотреть все сертификаты, используемые службами AD FS на сервере. Откройте Windows PowerShell и выполните следующую команду, чтобы добавить командлеты AD FS в сеанс Windows PowerShell: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Затем выполните следующую команду для просмотра всех сертификатов, используемых на сервере `PSH:>Get-ADFSCertificate`. Результат выполнения этой команды содержит значения StoreLocation и StoreName, указывающие на расположение хранилища каждого сертификата.  
  
> [!NOTE]
>  Кроме того, после этого можно воспользоваться инструкциями в статье [Экспорт части сертификата аутентификации сервера с закрытым ключом](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md) для экспорта каждого сертификата и его закрытого ключа в PFX-файл. Этот шаг не является обязательным, потому что все внешние сертификаты во время обновления операционной системы сохраняются.  
  
3. Создайте резервную копию файла конфигурации приложения. Вместе с другими параметрами этот файл содержит строку подключения к базе данных политик.  
  
Чтобы создать резервную копию файла конфигурации приложения, необходимо вручную скопировать файл `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` в надежное расположение на резервном сервере.  
  
> [!NOTE]
>  Запишите строку подключения к SQL Server после текста policystore connectionstring= в следующем файле:  `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`. Эта строка потребуется при восстановлении исходной конфигурации AD FS на сервере федерации.  
  
4. Запишите удостоверение учетной записи службы федерации AD FS 2.0 и пароль этой учетной записи.  
  
Чтобы найти значение удостоверения, просмотрите столбец **Вход от имени** **службы Windows AD FS 2.0** на консоли **Службы** . Запишите это значение вручную.  
  
## <a name="step-2-back-up-custom-attribute-stores"></a>Шаг 2. Резервное копирование хранилищ настраиваемых атрибутов  
 Сведения об используемых в AD FS хранилищах настраиваемых атрибутов можно найти с помощью Windows PowerShell. Откройте Windows PowerShell и выполните следующую команду, чтобы добавить командлеты AD FS в сеанс Windows PowerShell: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Затем выполните следующую команду, чтобы найти сведения о хранилищах настраиваемых атрибутов: `PSH:>Get-ADFSAttributeStore`. Действия по обновлению или переносу пользовательских хранилищ атрибутов могут быть разными.  
  
## <a name="step-3-back-up-webpage-customizations"></a>Шаг 3. Резервное копирование пользовательских настроек веб-страницы  
 Чтобы выполнить резервное копирование пользовательских настроек веб-страницы, копируйте веб-страницы AD FS и файл **web.config** из каталога, сопоставленного виртуальному пути **“/adfs/ls”** , в IIS. По умолчанию он находится в каталоге **%systemdrive%\inetpub\adfs\ls**.  
  
## <a name="next-steps"></a>Следующие шаги
 [Подготовка к миграции сервера AD FS 2.0 Federation](prepare-to-migrate-ad-fs-fed-server.md)   
 [Подготовка к миграции прокси-сервера AD FS 2.0 Federation](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Перенос сервера AD FS 2.0 Federation](migrate-the-ad-fs-fed-server.md)   
 [Перенос прокси-сервера AD FS 2.0 Federation](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Перенос веб-агентов AD FS 1.1](migrate-the-ad-fs-web-agent.md)