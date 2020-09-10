---
title: Миграция с Windows Small Business Server 2011 Essentials на Windows Server Essentials
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 32fc90d8-31c5-4c7e-9fe3-483cf3c35f78
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 7df1ca60ddd5bb89aa07819021bd3d11d213886f
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625816"
---
# <a name="migrate-windows-small-business-server-2011-essentials-to-windows-server-essentials"></a>Миграция с Windows Small Business Server 2011 Essentials на Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

В этом руководство описано, как перенести существующий домен Windows Small Business Server 2011 Essentials на Windows Server &reg; 2012 Essentials, а затем перенести параметры и данные. В этом руководство также описано, как удалить существующий сервер из сети Windows Server Essentials после завершения миграции.

> [!NOTE]
>  Чтобы избежать проблем во время миграции, Группа разработки продукта Windows Server Essentials настоятельно рекомендует ознакомиться с этим документом перед началом миграции.
>
> [!NOTE]
>
>  Сведения о переносе данных сервера в последнюю версию Windows Server Essentials см. в статье [Переход на Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).


## <a name="additional-resources"></a>Дополнительные ресурсы
 Ссылки на полезные при миграции дополнительные сведения, инструменты и ресурсы сообщества можно найти в разделе [Миграция Windows Small Business Server](https://go.microsoft.com/fwlink/?LinkId=217520).

## <a name="terms-and-definitions"></a>Термины и определения
 **Исходный сервер:** Существующий сервер, с которого переносятся параметры и данные.

 **Целевой сервер:** Новый сервер, на который переносятся параметры и данные.

## <a name="migration-process-summary"></a>Сводка по процессу миграции
 Настоящее руководство по миграции состоит из следующих разделов.


1.  [Подготовьте исходный сервер для миграции Windows Server Essentials](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Убедитесь, что исходный сервер и сеть готовы к миграции. В этом разделе подробно описаны архивация параметров исходного сервера, проверка работоспособности его системы, установка последних пакетов обновления и исправлений, а также проверка параметров сети.

2.  [Установите Windows Server Essentials в режиме миграции](Install-Windows-Server-Essentials-in-migration-mode.md).  В этом разделе описаны действия, которые необходимо выполнить для установки Windows Server Essentials на целевом сервере в режиме миграции.

3.  [Присоедините компьютеры к новому серверу Windows Server Essentials](Join-computers-to-the-new-Windows-Server-Essentials-server.md).  В этом разделе описывается присоединение клиентских компьютеров к новому серверу Windows Server Essentials и обновление параметров групповая политика.

4.  [Переместите параметры и данные SBS 2011 Essentials на целевой сервер](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md).  Этот раздел содержит сведения о переносе данных и параметров с исходного сервера.

5.  [Включите перенаправление папок на целевом сервере Windows Server Essentials](Enable-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Если перенаправление папок включено на исходном сервере, его можно включить на конечном сервере и затем удалить старый параметр групповой политики "Перенаправление папок".

6.  [Понизить и удалить исходный сервер из новой сети Windows Server Essentials](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Прежде чем удалить исходный сервер из сети, необходимо принудительно обновить групповую политику и понизить уровень исходного сервера.

7.  [Выполните задачи, выполняемые после миграции для Windows Server Essentials](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  После завершения переноса всех параметров и данных в Windows Server Essentials может потребоваться преобразовать разрешенные компьютеры в учетные записи пользователей.

8.  [Запустите анализатор соответствия рекомендациям Windows Server Essentials](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  После завершения переноса параметров и данных в Windows Server Essentials необходимо скачать и запустить анализатор соответствия рекомендациям Windows Server Essentials.

 Для выполнения некоторых процедур миграции нужно открыть окно командной строки от имени администратора.

###  <a name="to-open-a-command-prompt-window-on-the-source-server-as-an-administrator"></a><a name="BKMK_OpenACommandPromptAsAdmin"></a> Открытие окна командной строки на исходном сервере с правами администратора

1.  Щелкните **Запуск**.

2.  В поле поиска введите **cmd**.

3.  В списке результатов правой кнопкой мыши щелкните команду **cmd** и выберите пункт **Запуск от имени администратора**.

#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>Открытие окна командной строки на целевом сервере от имени администратора

1.  На **начальном экране** в поле поиска введите **cmd**.

2.  В списке результатов правой кнопкой мыши щелкните команду **cmd** и выберите пункт **Запуск от имени администратора**.
