---
title: Документация по выпуску Windows Server Essentials
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: db402a2b-7a46-448a-841c-750557cd12cc
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 9ef0e6bda6e66ab46824189219219dc1843cbe21
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622403"
---
# <a name="release-documentation-for-windows-server-essentials"></a>Документация по выпуску Windows Server Essentials

>Область применения: Windows Server 2016 Essentials

Добро пожаловать в документацию по выпуску сервера Windows Server 2016 Essentials. В этом разделе содержатся сведения о проблемах, которые могут возникнуть при установке и запуске серверного по Windows 2016 Server Essentials. Этот раздел следует изучить перед установкой и запуском Windows Server 2016 Essentials в сети.

## <a name="client-computers"></a>Клиентские компьютеры

### <a name="install-all-available-critical-and-security-updates-from-windows-update"></a>Установите все доступные критические обновления и обновления безопасности из Центра обновления Windows.

Перед подключением клиентского компьютера к серверу убедитесь, что вы открыли Центр обновления Windows на клиентском компьютере и установили все доступные критические обновления и исправления безопасности.

### <a name="client-computer-restore-may-not-succeed-after-migration-to-windows-10"></a>Восстановление клиентских компьютеров после миграции на Windows 10 может не выполняться
 После обновления клиентского компьютера с Windows 8.1 до Windows 10, восстановление клиентского компьютера может работать неправильно. Необходимо повторно подключить клиент к Windows Server 2016 Essentials.
