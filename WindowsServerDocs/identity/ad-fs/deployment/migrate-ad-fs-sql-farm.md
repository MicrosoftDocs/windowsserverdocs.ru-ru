---
title: Перенос фермы SQL сервера федерации AD FS 2,0
description: Содержит сведения о переносе фермы SQL Server AD FS 2,0 на сервер Windows Server 2012
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9882061aad5ec6620cda5a0a288790d34f25c3f3
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966676"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>Перенос фермы AD FS 2,0 WID  
В этом документе содержатся подробные сведения о миграции фермы SQL AD FS 2,0 на сервер Windows Server 2012.


## <a name="migrate-a-sql-server-farm"></a>Миграция фермы SQL Server  
 Чтобы перенести SQL Server ферму на Windows Server 2012, выполните следующую процедуру:  
  
1.  Для каждого сервера в SQL Server ферме проверьте и выполните процедуры, описанные в подразделе [миграция SQL Server фермы](prepare-to-migrate-a-sql-server-farm.md).  
  
2.  Удалите из балансировщика нагрузки все серверы фермы SQL Server.  
  
3.  Обновите операционную систему на этом сервере в ферме SQL Server с Windows Server 2008 R2 или Windows Server 2008 до Windows Server 2012. Дополнительные сведения см. в разделе [Установка Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11)).  
  
> [!IMPORTANT]
>  В результате обновления ОС конфигурация AD FS на этом сервере была утрачена, а роль сервера AD FS 2.0 — удалена. Вместо этого устанавливается роль сервера AD FS Windows Server 2012, но она не настроена. Необходимо вручную создать исходную конфигурацию AD FS и восстановить остальные параметры AD FS, чтобы завершить миграцию сервера федерации.  
  
4. Создайте оригинальную конфигурацию AD FS на этом сервере фермы SQL Server, воспользовавшись командлетами AD FS Windows PowerShell для добавления сервера на существующую ферму.  
  
> [!IMPORTANT]
>  Следует воспользоваться Windows PowerShell для создания исходной конфигурации AD FS, если для хранения базы данных конфигурации AD FS используется SQL Server.  

  - Откройте Windows PowerShell и выполните следующую команду: `$fscredential = Get-Credential` .  
  - Введите имя и пароль учетной записи службы, записанные в ходе подготовки фермы серверов SQL к миграции.  
  - Выполните следующую команду: `Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"` , где `Data Source` — это значение источника данных в строке подключения к хранилищу политик в следующем файле: `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` .  
  
5. Добавьте только что обновленный сервер до Windows Server 2012 в подсистему балансировки нагрузки.  
  
6. Повторите шаги 2–6 для остальных узлов на ферме SQL Server.  
  
7. Когда все серверы в ферме SQL Server обновлены до Windows Server 2012, восстановите оставшиеся AD FS настройки, например пользовательские хранилища атрибутов.  

## <a name="next-steps"></a>Дальнейшие шаги
 [Подготовка к миграции сервера федерации AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md)   
 [Подготовка к миграции прокси-сервера AD FS 2,0 Федерации](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Перенос сервера федерации AD FS 2,0](migrate-the-ad-fs-fed-server.md)   
 [Перенос прокси-сервера AD FS 2,0 Федерации](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Перенос веб-агентов AD FS 1.1](migrate-the-ad-fs-web-agent.md)
