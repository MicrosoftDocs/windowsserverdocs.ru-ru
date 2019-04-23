---
title: Матрица обновления и миграции ролей сервера для Windows Server 2016
description: Показывает, какие роли сервера можно обновить или перенести на Windows Server 2016.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 10/05/2016
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e031a64-b1e6-4cf6-994a-e7c575835f6a
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 9f8310baf659810d5d51587bafcc868c59ace61a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852055"
---
# <a name="server-role-upgrade-and-migration-matrix-for-windows-server-2016"></a>Матрица обновления и миграции ролей сервера для Windows Server 2016

>Область применения. Windows Server 2016

Таблица на этой странице описывает варианты обновления и миграции для ролей сервера, касающиеся перехода на Windows Server 2016. Указания по миграции отдельных ролей см. в статье [Миграция ролей и функций в Windows Server](https://docs.microsoft.com/windows-server/get-started/migrate-roles-and-features). Дополнительные сведения об установке и обновлении см. в статье [Установка, обновление и миграция Windows Server](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade).

|Роль сервера|Возможно ли обновление с Windows Server 2012 R2?|Возможно ли обновление с Windows Server 2012?|Поддерживается ли миграция?|Можно ли выполнить миграцию без простоя?|  
|-------------------|----------|--------------|--------------|----------|  
|Службы сертификатов Active Directory| Да|    Да|    Да|    Нет|
|Доменные службы Active Directory|  Да|    Да|    Да|    Да|
|Службы федерации Active Directory (AD FS)|  Нет| Нет| Да|    Нет (в ферму нужно добавить новые узлы)|
|Службы Active Directory облегченного доступа к каталогам (AD LDS)|   Да|    Да|    Да|    Да|
|Службы управления правами Active Directory (AD RMS)|   Да|    Да|    Да|    Нет|
|DHCP-сервер|   Да|    Да|    Да|    Да|
|DNS-сервер|    Да|    Да|    Да|    Нет|
|Отказоустойчивый кластер|Да, с помощью процедуры [последовательного обновления кластерной ОС](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade), включающей в себя приостановку и прекращение, исключение, обновление до Windows Server 2016 и повторное присоединение к исходному кластеру. Да, когда сервер удаляется кластером для обновления, а затем добавляется в другой кластер.|Нет, пока сервер является частью кластера. Да, когда сервер удаляется кластером для обновления, а затем добавляется в другой кластер.  |Да|Нет, для отказоустойчивых кластеров Windows Server 2012. Да, для отказоустойчивых кластеров Windows Server 2012 R2 с виртуальными машинами Hyper-V или отказоустойчивых кластеров Windows Server 2012 R2, где запущена роль масштабируемого файлового сервера. См. статью [Последовательное обновление кластерной ОС](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade).|
|Файловые службы и службы хранилища| Да|    Да|    Зависит от подкомпонента|  Нет|
|Hyper-V| Да. (Когда узел является частью кластера, используется процедура последовательного обновления кластерной ОС, включающая в себя приостановку и прекращение, исключение, обновление до Windows Server 2016 и повторное присоединение к исходному кластеру.)|  Нет|   Да|  Нет, для отказоустойчивых кластеров Windows Server 2012. Да, для отказоустойчивых кластеров Windows Server 2012 R2 с виртуальными машинами Hyper-V или отказоустойчивых кластеров Windows Server 2012 R2, где запущена роль масштабируемого файлового сервера. См. статью [Последовательное обновление кластерной ОС](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade).| 
|Службы печати и факсов|    Нет| Нет| Да (Printbrm.exe)| Нет|
|Службы удаленных рабочих столов|   Да, для всех подчиненных ролей, но ферма в смешанном режиме не поддерживается|   Да, для всех подчиненных ролей, но ферма в смешанном режиме не поддерживается|   Да|    Нет|
|Веб-сервер (IIS)|  Да|    Да|    Да|    Нет|
|Режим Windows Server Essentials|  Да|    Н/Д — новая функция|  Да|    Нет|
|Службы Windows Server Update Services|    Да|    Да|    Да|    Нет|
|рабочие папки|  Да|    Да|    Да|    Да, из кластера Windows Server 2012 R2 при использовании [последовательного обновления кластерной ОС](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade).|

