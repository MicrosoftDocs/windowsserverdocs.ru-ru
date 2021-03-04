---
title: DirectAccess
description: Этот раздел можно использовать для краткого обзора DirectAccess в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 6b71d18e-1939-4fc0-bb42-29e0e5ffc8da
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: cb24671451f7a22bf6dc29001f82d040ef46b018
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101832289"
---
# <a name="directaccess"></a>DirectAccess

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

Этот раздел содержит краткий обзор DirectAccess, включая серверные и клиентские операционные системы, поддерживающие DirectAccess, а также ссылки на дополнительную документацию по DirectAccess для Windows Server 2016.

> [!NOTE]
> Помимо этого раздела, доступна следующая документация по DirectAccess.
>
> -   [Пути развертывания DirectAccess в Windows Server](DirectAccess-Deployment-Paths-in-Windows-Server.md)
> -   [Предварительные требования для развертывания DirectAccess](Prerequisites-for-Deploying-DirectAccess.md)
> -   [Неподдерживаемые конфигурации DirectAccess](DirectAccess-Unsupported-Configurations.md)
> -   [Руководства по лаборатории тестирования DirectAccess](DirectAccess-Test-Lab-Guides.md)
> -   [DirectAccess — известные проблемы](DirectAccess-Known-Issues.md)
> -   [Планирование загрузки DirectAccess](DirectAccess-Capacity-Planning.md)
> -   [Автономное присоединение к домену DirectAccess](DirectAccess-Offline-Domain-Join.md)
> -   [Диагностика DirectAccess](Troubleshooting-DirectAccess.md)
> -   [Развертывание одного сервера DirectAccess с помощью мастера начало работы](single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)
> -   [Развертывание одного сервера DirectAccess с расширенными параметрами](single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)
> -   [Добавление DirectAccess в существующее развертывание удаленного доступа (VPN)](add-to-existing-vpn/Add-DirectAccess-to-an-Existing-Remote-Access-VPN-Deployment.md)

DirectAccess позволяет удаленным пользователям подключаться к сетевым ресурсам Организации без необходимости в традиционных подключениях к виртуальной частной сети (VPN). При использовании подключений DirectAccess удаленные клиентские компьютеры всегда подключены к вашей организации. удаленным пользователям не нужно запускать и прекращать подключения, как это необходимо для VPN-подключений. Кроме того, ИТ администраторы могут управлять клиентскими компьютерами DirectAccess, когда они работают и подключены к Интернету.

>[!IMPORTANT]
>Не пытайтесь развернуть удаленный доступ на виртуальной машине виртуальной машины \( \) в Microsoft Azure. Использование удаленного доступа в Microsoft Azure не поддерживается. Удаленный доступ на виртуальной машине Azure нельзя использовать для развертывания VPN, DirectAccess или любой другой функции удаленного доступа в Windows Server 2016 или более ранних версиях Windows Server. Дополнительные сведения см. в [статье поддержка серверного программного обеспечения Майкрософт для Microsoft Azure виртуальных машин](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

DirectAccess обеспечивает поддержку только для присоединенных к домену клиентов, включающих поддержку операционной системы для DirectAccess.

Следующие серверные операционные системы поддерживают DirectAccess.

-   Вы можете развернуть все версии Windows Server 2016 в качестве клиента DirectAccess или сервера DirectAccess.

-   Можно развернуть все версии Windows Server 2012 R2 в качестве клиента DirectAccess или сервера DirectAccess.

-   Вы можете развернуть все версии Windows Server 2012 в качестве клиента DirectAccess или сервера DirectAccess.

-   Можно развернуть все версии Windows Server 2008 R2 в качестве клиента DirectAccess или сервера DirectAccess.

Следующие клиентские операционные системы поддерживают DirectAccess.

-   Windows 10 Корпоративная

-   Windows 10 Корпоративная 2015 Long Term Servicing Branch (LTSB)

-   Windows 8 и 8,1 Enterprise

-   Windows 7 Максимальная

-   Windows 7 Корпоративная
