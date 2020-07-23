---
ms.assetid: 222e9f93-7c41-4527-8a98-8f7fbc7a58af
title: Развертывание прокси-серверов федерации
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 445f3b6fef526cb5dd308be8aafe49a3ecddd6a4
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965976"
---
# <a name="deploying-federation-server-proxies"></a>Развертывание прокси-серверов федерации

В службы федерации Active Directory (AD FS) \( AD FS \) в Windows Server 2012 R2 роль прокси-сервера федерации обрабатывается новой службой роли удаленного доступа под названием прокси-приложение. Чтобы обеспечить доступность AD FS для доступа извне корпоративной сети, которая была предназначена для развертывания прокси-сервера федерации в устаревших версиях AD FS, таких как AD FS 2,0 и AD FS в Windows Server 2012, можно развернуть один или несколько прокси веб-приложений для AD FS в Windows Server 2012 R2.  
  
В контексте AD FS прокси веб-приложения функционирует в качестве прокси-сервера AD FS Федерации. Кроме того, прокси-сервер веб-приложения предоставляет функции обратного прокси-сервера для веб-приложений в корпоративной сети, что делает их доступными для пользователей с любых устройств из-за пределов корпоративной сети. Дополнительные сведения о службе роли прокси веб-приложения см. в разделе "Обзор прокси-сервера веб-приложения".  
  
При планировании развертывания прокси-сервера веб-приложения можно использовать сведения из следующих разделов.  
  
-   [Планирование инфраструктуры прокси веб-приложений (WAP)](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))  
  
-   [Планирование прокси-сервера веб-приложений](/previous-versions/orphan-topics/ws.11/dn383647(v=ws.11))  
  
При развертывании прокси-сервера веб-приложения можно следовать процедурам в следующих разделах.  
  
-   [Настройка инфраструктуры прокси-сервера веб-приложений](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383644(v=ws.11))  
  
-   [Установка и настройка прокси-сервера веб-приложений](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383662(v=ws.11))  
  
 
## <a name="see-also"></a>См. также: 

[Развертывание AD FS](../../ad-fs/AD-FS-Deployment.md)  

[Руководство по развертыванию служб федерации Active Directory в Windows Server 2012 R2](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Развертывание фермы серверов федерации](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
