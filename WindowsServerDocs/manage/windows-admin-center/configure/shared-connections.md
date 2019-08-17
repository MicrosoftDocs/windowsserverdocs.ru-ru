---
title: Настройка общих подключений для всех пользователей шлюза центра администрирования Windows
description: Узнайте, как администраторы могут настроить шлюз Windows Admin Center (Project Хонолулу) один раз, чтобы позволить всем пользователям совместно использовать один список подключений.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 46075154a225590376458881768ae86f74a572ad
ms.sourcegitcommit: 286e3181ebd2cb9d7dc7fe651858a4e0d61d153f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2019
ms.locfileid: "68300726"
---
# <a name="configure-shared-connections-for-all-users-of-the-windows-admin-center-gateway"></a>Настройка общих подключений для всех пользователей шлюза центра администрирования Windows

> Область применения. Предварительная версия центра администрирования Windows, центр администрирования Windows

С возможностью настройки общих подключений администраторы шлюзов могут настроить список подключений один раз для всех пользователей данного шлюза центра администрирования Windows. 

На вкладке **Общие подключения** параметров шлюза центра администрирования Windows Администраторы шлюзов могут добавлять серверы, кластеры и подключения к ПК, как это было бы на странице все подключения, включая возможность добавления тегов к подключениям. Все подключения и теги, добавленные в списке Общие подключения, будут отображаться для всех пользователей этого шлюза центра администрирования Windows со страницы все подключения.
    ![](../media/shared-cnxns-1.png)

Когда любой пользователь центра администрирования Windows получает доступ к странице "все подключения" после настройки общих подключений, они увидят подключения, сгруппированные по двум разделам: Личные и общие подключения. Личная группа является списком подключений конкретного пользователя и сохраняется в сеансах браузера этого пользователя. Группа общие подключения одинакова для всех пользователей и не может быть изменена на странице все подключения.
![](../media/shared-cnxns-2.png)