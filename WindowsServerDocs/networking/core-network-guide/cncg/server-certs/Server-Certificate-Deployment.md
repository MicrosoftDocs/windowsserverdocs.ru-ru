---
title: Развертывание сертификата сервера
description: Сведения о шагах, которые необходимо выполнить для установки корневого центра сертификации предприятия и развертывании сертификатов сервера для использования с PEAP и EAP.
manager: brianlic
ms.topic: article
ms.assetid: 1ae4384b-f4e4-41e8-bc5f-9ac41953bca4
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 5e1c79160df359f57bdc4a243874b06716a19ffc
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825471"
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



