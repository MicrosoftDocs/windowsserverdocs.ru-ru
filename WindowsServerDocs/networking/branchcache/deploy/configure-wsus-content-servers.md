---
title: Настройка серверов содержимого служб Windows Server Update Services (WSUS)
description: Эта статья является частью руководства по развертыванию BranchCache для Windows Server 2016, в котором демонстрируется развертывание службы BranchCache в распределенном и размещенном режимах кэша для оптимизации использования пропускной способности глобальной сети в филиалах.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0662a72f23a06e62d92fc040aa88e11f795083e3
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990164"
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Настройка серверов содержимого служб Windows Server Update Services (WSUS)

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

После установки компонента BranchCache и запуска службы BranchCache серверы WSUS должны быть настроены для хранения файлов обновления на локальном компьютере.

При настройке серверов WSUS для хранения файлов обновления на локальном компьютере метаданные обновлений и файлы обновления загружаются и хранятся непосредственно на сервере WSUS. Это гарантирует получение клиентскими компьютерами службы BranchCache файлов обновления продуктов Майкрософт с сервера WSUS, а не непосредственно с веб-сайта Центр обновления Майкрософт.

Дополнительные сведения о синхронизации WSUS см. в разделе [Настройка синхронизации обновлений](../../../administration/windows-server-update-services/manage/setting-up-update-synchronizations.md) .