---
title: Настройка серверов содержимого служб Windows Server Update Services (WSUS)
description: Узнайте, как настроить серверы содержимого Windows Server Update Services (WSUS) для хранения файлов обновлений на локальном компьютере.
manager: brianlic
ms.topic: how-to
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: jgerend
author: JasonGerend
ms.date: 01/05/2021
ms.openlocfilehash: 7d02f1cfbe38d69985874be2b873b8403c34139f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101830227"
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Настройка серверов содержимого служб Windows Server Update Services (WSUS)

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

После установки компонента BranchCache и запуска службы BranchCache серверы WSUS должны быть настроены для хранения файлов обновления на локальном компьютере.

При настройке серверов WSUS для хранения файлов обновления на локальном компьютере метаданные обновлений и файлы обновления загружаются и хранятся непосредственно на сервере WSUS. Это гарантирует получение клиентскими компьютерами службы BranchCache файлов обновления продуктов Майкрософт с сервера WSUS, а не непосредственно с веб-сайта Центр обновления Майкрософт.

Дополнительные сведения о синхронизации WSUS см. в разделе [Настройка синхронизации обновлений](../../../administration/windows-server-update-services/manage/setting-up-update-synchronizations.md) .