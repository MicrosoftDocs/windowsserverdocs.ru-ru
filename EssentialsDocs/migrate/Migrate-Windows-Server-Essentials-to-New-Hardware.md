---
title: Миграция с Windows Server Essentials на новое оборудование
description: Узнайте, как перенести существующий домен Windows Server 2012 Essentials на Windows Server Essentials на новом оборудовании, а затем перенести параметры и данные.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: f695ae90-3160-407b-bebf-9e460f22c86d
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: d95100cdfa08fa1aa672be8c9978ac230573a46c
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810901"
---
# <a name="migrate-windows-server-essentials-to-new-hardware"></a>Миграция с Windows Server Essentials на новое оборудование

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

В этом руководство описано, как перенести существующий домен Windows Server &reg; 2012 Essentials в Windows Server Essentials на новом оборудовании, а затем перенести параметры и данные. В этом руководство также описано, как удалить существующий сервер из сети Windows Server Essentials после завершения миграции.

> [!NOTE]
>  Чтобы избежать проблем во время миграции, Группа разработки продукта Windows Server Essentials настоятельно рекомендует ознакомиться с этим документом перед началом миграции.
>
> [!NOTE]
>
>  Сведения о переносе данных сервера в последнюю версию Windows Server Essentials см. в статье [Переход на Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).


## <a name="additional-resources"></a>Дополнительные ресурсы
 Ссылки на полезные при миграции дополнительные сведения, инструменты и ресурсы сообщества можно найти на веб-сайте о [миграции Windows Small Business Server](https://go.microsoft.com/fwlink/?LinkId=217520).

## <a name="terms-and-definitions"></a>Термины и определения
 **Исходный сервер:** Существующий сервер, с которого переносятся параметры и данные.

 **Целевой сервер:** Новый сервер, на который переносятся параметры и данные.

## <a name="migration-process-summary"></a>Сводка по процессу миграции
 Настоящее руководство по миграции состоит из следующих разделов.


1. [Подготовьте исходный сервер для миграции Windows Server Essentials](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Убедитесь, что исходный сервер и сеть готовы к миграции. В этом разделе подробно описаны архивация параметров исходного сервера, проверка работоспособности его системы, установка последних пакетов обновления и исправлений, а также проверка параметров сети.

2. [Установите Windows Server Essentials в режиме миграции](Install-Windows-Server-Essentials-in-migration-mode.md).  В этом разделе описаны действия, которые необходимо выполнить для установки Windows Server Essentials на целевом сервере в режиме миграции.

3. [Присоедините компьютеры к новому серверу Windows Server Essentials](Join-computers-to-the-new-Windows-Server-Essentials-server.md).  В этом разделе описывается присоединение клиентских компьютеров к новому серверу Windows Server Essentials и обновление параметров групповая политика.

4. [Переместите параметры и данные на целевой сервер для миграции Windows Server Essentials](Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Этот раздел содержит сведения о переносе данных и параметров с исходного сервера.

5. [Настройте перенаправление папок на целевом сервере Windows Server Essentials](Configure-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Если перенаправление папок включено на исходном сервере, его можно включить на конечном сервере и затем удалить старый параметр групповой политики "Перенаправление папок".

6. [Понизить и удалить исходный сервер из новой сети Windows Server Essentials](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Прежде чем удалить исходный сервер из сети, необходимо принудительно обновить групповую политику и понизить уровень исходного сервера.

7. [Выполните задачи, выполняемые после миграции для Windows Server Essentials](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  После завершения переноса всех параметров и данных в Windows Server Essentials может потребоваться преобразовать разрешенные компьютеры в учетные записи пользователей.

8. [Запустите анализатор соответствия рекомендациям Windows Server Essentials](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  После завершения переноса параметров и данных в Windows Server Essentials необходимо скачать и запустить анализатор соответствия рекомендациям Windows Server Essentials.

   Для выполнения некоторых процедур миграции нужно открыть окно командной строки от имени администратора.

#### <a name="to-open-a-command-prompt-window-as-an-administrator"></a>Открытие окна командной строки от имени администратора

1.  На **начальном экране** в поле поиска введите **cmd**.

2.  В списке результатов правой кнопкой мыши щелкните команду **cmd** и выберите пункт **Запуск от имени администратора**.
