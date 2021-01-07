---
title: Настройка серверов содержимого служб Windows Server Update Services (WSUS)
description: Узнайте, как настроить серверы содержимого Windows Server Update Services (WSUS) для хранения файлов обновлений на локальном компьютере.
manager: brianlic
ms.topic: how-to
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: 9e55b470df3d1fc3eed8a69d89b228d3d7b7ed70
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950410"
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Настройка серверов содержимого служб Windows Server Update Services (WSUS)

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

После установки компонента BranchCache и запуска службы BranchCache серверы WSUS должны быть настроены для хранения файлов обновления на локальном компьютере.

При настройке серверов WSUS для хранения файлов обновления на локальном компьютере метаданные обновлений и файлы обновления загружаются и хранятся непосредственно на сервере WSUS. Это гарантирует получение клиентскими компьютерами службы BranchCache файлов обновления продуктов Майкрософт с сервера WSUS, а не непосредственно с веб-сайта Центр обновления Майкрософт.

Дополнительные сведения о синхронизации WSUS см. в разделе [Настройка синхронизации обновлений](../../../administration/windows-server-update-services/manage/setting-up-update-synchronizations.md) .