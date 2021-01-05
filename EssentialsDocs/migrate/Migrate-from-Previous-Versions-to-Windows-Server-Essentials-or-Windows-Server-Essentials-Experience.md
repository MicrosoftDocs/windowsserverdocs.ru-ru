---
title: Миграция с предыдущих версий на Windows Server Essentials или Windows Server Essentials Experience
description: Узнайте, как выполнить миграцию с предыдущих версий Windows Small Business Server и Windows Server Essentials.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 2974fb3a-5150-43fd-a73f-3e5074eb5d03
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: e25e8407e960264387ba946d11b721b3b22014bf
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810761"
---
# <a name="migrate-from-previous-versions-to-windows-server-essentials-or-windows-server-essentials-experience"></a>Миграция с предыдущих версий на Windows Server Essentials или Windows Server Essentials Experience

>Область применения: Windows Server 2012 R2 Essentials

В этом руководство описано, как выполнить миграцию с предыдущих версий Windows Small Business Server и Windows Server Essentials (включая Windows Server Essentials, Windows Small Business Server 2011 Standard, Windows Small Business Server 2011 Essentials, Windows Small Business Server 2008 и Windows Small Business Server 2003) в Windows Server Essentials или на Windows Server 2012 R2 с установленной ролью Windows Server Essentials Experience.

 **Для сред, в которых до 25 пользователей и устройств 50**, можно выполнить действия, описанные в этом руководстве, для перехода с предыдущих версий Windows SBS на Windows Server Essentials.

 **Для сред, в которых 100 пользователей и 200 устройств**, можно использовать те же рекомендации для перехода на стандартные или выпуски Datacenter в windows Server 2012 R2 с установленной ролью Windows Server Essentials Experience.

> [!NOTE]
>  Во избежание проблем во время миграции группа разработки продукта Windows Server Essentials настоятельно рекомендует ознакомиться с этим документом перед началом миграции.

## <a name="terms-and-definitions"></a>Термины и определения
 **Исходный сервер:** существующий сервер, с которого выполняется миграция параметров и данных.

 **Целевой сервер:** новый сервер, на который выполняется миграция параметров и данных.

## <a name="migration-process-summary"></a>Сводка по процессу миграции
 Настоящее руководство по миграции состоит из следующих разделов:

1. [Шаг 1. Подготовка исходного сервера к переходу на Windows Server Essentials](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Убедитесь, что исходный сервер и сеть готовы к миграции. В этом разделе подробно описаны архивация параметров исходного сервера, проверка работоспособности его системы, установка последних пакетов обновления и исправлений, а также проверка параметров сети.

2. [Шаг 2. Установите Windows Server Essentials как новый контроллер домена реплики](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md). В этом разделе описывается установка Windows Server Essentials или Windows Server 2012 R2 Standard (с включенной ролью Windows Server Essentials) в качестве контроллера домена.

3. [Шаг 3. Присоединение компьютеров к новому серверу Windows Server Essentials](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md).  В этом разделе объясняется, как присоединить клиентские компьютеры к новому серверу под управлением Windows Server Essentials и обновить параметры групповая политика.

4. [Шаг 4. Перемещение параметров и данных на целевой сервер для миграции Windows Server Essentials](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Этот раздел содержит сведения о переносе данных и параметров с исходного сервера.

5. [Шаг 5. Включите перенаправление папок на целевом сервере для миграции Windows Server Essentials](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Если перенаправление папок включено на исходном сервере, его можно включить на конечном сервере и затем удалить старый параметр групповой политики "Перенаправление папок".

6. [Шаг 6. понизить и удалите исходный сервер из новой сети Windows Server Essentials](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Прежде чем удалить исходный сервер из сети, необходимо принудительно обновить групповую политику и понизить уровень исходного сервера.

7. [Шаг 7. выполнение задач, выполняемых после миграции Windows Server Essentials](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md).  После завершения переноса всех параметров и данных в Windows Server Essentials может потребоваться преобразовать разрешенные компьютеры в учетные записи пользователей.

8. [Шаг 8. запуск анализатор соответствия рекомендациям Windows Server Essentials](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  После завершения миграции параметров и данных в Windows Server Essentials следует запустить Windows Server Essentials анализатор соответствия рекомендациям (BPA).

   Для выполнения некоторых процедур миграции нужно открыть окно командной строки от имени администратора. Ниже описано, как это сделать.

###  <a name="to-open-a-command-prompt-window-on-the-source-server-as-an-administrator"></a><a name="BKMK_OpenACommandPromptAsAdmin"></a> Открытие окна командной строки на исходном сервере с правами администратора

1.  Щелкните **Запуск**.

2.  В поле поиска введите **cmd**.

3.  В списке результатов правой кнопкой мыши щелкните команду **cmd** и выберите пункт **Запуск от имени администратора**.

#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>Открытие окна командной строки на конечном сервере от имени администратора

1.  На **начальном экране** в поле поиска введите **cmd**.

2.  В списке результатов правой кнопкой мыши щелкните команду **cmd** и выберите пункт **Запуск от имени администратора**.

## <a name="additional-references"></a>Дополнительные ссылки

-   [Перенос данных сервера в Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

