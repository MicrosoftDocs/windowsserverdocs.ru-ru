---
title: Развертывание сертификата сервера
description: Эта статья является частью руководств по развертыванию сертификатов сервера для беспроводных и беспроводных развертываний 802.1 X.
manager: brianlic
ms.topic: article
ms.assetid: 1ae4384b-f4e4-41e8-bc5f-9ac41953bca4
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 09b5ec45562a2ecd60c8ab1a753b9d917b6cdfd9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949338"
---
# <a name="server-certificate-deployment"></a>Развертывание сертификата сервера

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Выполните следующие действия, чтобы установить корневой центр сертификации (ЦС) предприятия и развернуть сертификаты сервера для использования с протоколами PEAP и EAP.

> [!IMPORTANT]
> Перед установкой служб Active Directory сертификатов необходимо присвоить компьютеру имя, настроить компьютер со статическим IP-адресом и присоединить компьютер к домену. После установки служб AD CS нельзя изменить имя компьютера или членство в домене компьютера, однако при необходимости можно изменить IP-адрес. Дополнительные сведения о выполнении этих задач см. в разделе &reg; [сетевого руководства](../../Core-Network-Guide.md)по Windows Server 2016 Core.


-   [Установка веб-сервера WEB1](../../../core-network-guide/cncg/server-certs/Install-the-Web-Server-WEB1.md)

-   [Создание записи псевдонима (CNAME) в DNS для WEB1](../../../core-network-guide/cncg/server-certs/Create-an-Alias-CNAME-Record-in-DNS-for-WEB1.md)

-   [Настройка WEB1 для распространения списков отзыва сертификатов (CRL)](../../../core-network-guide/cncg/server-certs/Configure-WEB1-to-Distribute-Certificate-Revocation-Lists.md)

-   [Подготовка INF-файла CAPolicy](../../../core-network-guide/cncg/server-certs/Prepare-the-CAPolicy-inf-File.md)

-   [Установка центра сертификации](../../../core-network-guide/cncg/server-certs/Install-the-Certification-Authority.md)

-   [Настройка расширений CDP и AIA в CA1](../../../core-network-guide/cncg/server-certs/Configure-the-CDP-and-AIA-Extensions-on-CA1.md)

-   [Копирование сертификата ЦС и списка отзыва сертификатов в виртуальный каталог](../../../core-network-guide/cncg/server-certs/Copy-the-CA-Certificate-and-CRL-to-the-Virtual-Directory.md)

-   [Настройка шаблона сертификата сервера](../../../core-network-guide/cncg/server-certs/Configure-the-Server-Certificate-Template.md)

-   [Настройка автоматической регистрации сертификатов сервера](../../../core-network-guide/cncg/server-certs/Configure-Server-Certificate-Autoenrollment.md)

-   [Обновить групповая политика](../../../core-network-guide/cncg/server-certs/Refresh-Group-Policy.md)

-   [Проверка регистрации сервера сертификата сервера](../../../core-network-guide/cncg/server-certs/Verify-Server-Enrollment-of-a-Server-Certificate.md)

> [!NOTE]
> Процедуры, описанные в этом разделе, не включают инструкции для случаев, когда открывается диалоговое окно " **контроль учетных записей пользователей** " для запроса на продолжение. Если во время выполнения процедур, описанных в данном руководстве, отображается это диалоговое окно, и если оно отображается в ответ на ваше действие, нажмите кнопку **Продолжить**.



