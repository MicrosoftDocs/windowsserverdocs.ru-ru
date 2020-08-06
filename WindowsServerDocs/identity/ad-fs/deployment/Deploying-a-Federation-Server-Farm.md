---
ms.assetid: bbb5b68f-00ad-4715-8176-0c2769b706c4
title: Развертывание фермы серверов федерации для Windows Server 2012 R2 AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9ad0ad65b05f9f01793bcc2f6732edfa8372a021
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864213"
---
# <a name="deploying-a-federation-server-farm"></a>Развертывание фермы серверов федерации

Для развертывания фермы серверов федерации выполните задачи из этого контрольного списка в указанном порядке. Если ссылка приведет вас на концептуальную статью, вернитесь к этому контрольному списку после ее просмотра, чтобы вы могли продолжить выполнять оставшиеся задачи контрольного списка.

![Контрольный список развертывания фермы федеративных серверов](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**: развертывание фермы серверов федерации**

|Задача|Справочник|
|--------|-------------|
|Изучите важные понятия и рекомендации по мере подготовки к развертыванию службы федерации Active Directory (AD FS) \( AD FS \) . **Примечание**.|![развертывание интегрированной фермы серверов](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS руководство по проектированию в Windows server 2012 R2](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)<p>![Основные](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[понятия о ключевых AD FS](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md) развертывании фермы федеративных серверов|
||Если вы решили использовать Microsoft SQL Server для хранилища конфигурации AD FS, убедитесь, что развернут функциональный экземпляр SQL Server.|Предупреждение [SQL Server](/sql/sql-server/?view=sql-server-ver15) **.** в Windows Server 2012 R2 если вы хотите создать ферму AD FS и использовать SQL Server для хранения данных конфигурации, можно использовать SQL Server 2008 и более новые версии, включая SQL Server 2012.|
|Присоедините компьютер к домену Active Directory.|![Развертывание федеративной фермы серверов](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Присоединение компьютера к домену](Join-a-Computer-to-a-Domain.md)|
|Регистрация SSL-сертификата на уровне SSL \( \) для AD FS.|![Развертывание федеративной фермы серверов](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Регистрация SSL-сертификата для AD FS](Enroll-an-SSL-Certificate-for-AD-FS.md)|
|Установите службу роли AD FS.|![Развертывание федеративной фермы серверов](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Установка службы роли AD FS](Install-the-AD-FS-Role-Service.md)|
|Настройте сервер федерации.|![Развертывание федеративной фермы серверов](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Настройка сервера федерации](Configure-a-Federation-Server.md)|
|Необязательный шаг. Настройте сервер федерации с помощью DRS службы регистрации устройств \( \) .|![Развертывание федеративной фермы серверов](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Настройка сервера федерации с помощью службы регистрации устройств](Configure-a-federation-server-with-Device-Registration-Service.md)|
|Добавьте \( \) запись ресурса a и псевдонима \( CNAME \) в корпоративную службу доменных имен \( (DNS) \) для службы федерации и DRS.|![Развертывание федеративной фермы серверов](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Настройка корпоративных DNS для служба Федерации и DRS](Configure-Corporate-DNS-for-the-Federation-Service-and-DRS.md)|
|Проверьте работоспособность сервера федерации.|![Развертывание федеративной фермы серверов](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Проверка работоспособности сервера федерации](Verify-That-a-Federation-Server-Is-Operational.md)|


## <a name="see-also"></a>См. также:
[Развертывание AD FS](../../ad-fs/AD-FS-Deployment.md)

[Руководство по развертыванию служб федерации Active Directory в Windows Server 2012 R2](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)

