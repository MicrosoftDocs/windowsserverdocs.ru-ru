---
title: Настройка задачи "Зарегистрироваться в Microsoft Online Backup Service"
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: a7eafbb3-7728-487e-b287-90bbd6fee7f0
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: c424be2d0815fbcb217e0453b27f4b7aceb07ee6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623636"
---
# <a name="customize-sign-up-for-microsoft-online-backup-service-task"></a>Настройка задачи "Зарегистрироваться в Microsoft Online Backup Service"

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

По умолчанию при выборе задачи **Зарегистрироваться на Microsoft Online Backup Service** на вкладке **УСТРОЙСТВА** панели мониторинга открывается веб-сайт Microsoft Online Backup Service. На веб-сайте представлена информация о службе, предоставляется помощь в регистрации и загрузке необходимого программного обеспечения.

 Изменить настройки задачи **Зарегистрироваться на Microsoft Online Backup Service** можно двумя способами:

-   Можно заменить URL-адрес веб-сайта по умолчанию на URL-адрес, представляющий особое взаимодействие с пользователем. Чтобы изменить URL-адрес по умолчанию, откройте редактор реестра и создайте раздел реестра: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\LinkUrl**, а затем назначьте пользовательский URL-адрес в качестве значения реестра.

-   Задачу можно скрыть. Чтобы скрыть задачу, откройте редактор реестра и создайте раздел реестра: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\OnlineBackupInstalled**.

## <a name="see-also"></a>См. также:
 [Создание и Настройка образа](Creating-and-Customizing-the-Image.md) [Дополнительные настройки](Additional-Customizations.md) [Подготовка образа для развертывания](Preparing-the-Image-for-Deployment.md) [Тестирование взаимодействия с пользователем](Testing-the-Customer-Experience.md)