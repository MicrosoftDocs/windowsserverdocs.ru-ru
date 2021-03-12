---
title: Документация по выпуску Windows Server Essentials
description: Узнайте о том, что входит в выпуск Windows Server 2016 Essentials.
ms.date: 03/10/2021
ms.topic: article
ms.assetid: db402a2b-7a46-448a-841c-750557cd12cc
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: f2ddd44268ebf5e07d13fcfe237dba07c7b96ed3
ms.sourcegitcommit: dea7efcf78e88094cd4c2f2288191eb76a3ec229
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/10/2021
ms.locfileid: "102622332"
---
# <a name="release-documentation-for-windows-server-essentials"></a>Документация по выпуску Windows Server Essentials

>Область применения: Windows Server 2016 Essentials

Добро пожаловать в документацию по выпуску сервера Windows Server 2016 Essentials. В этом разделе содержатся сведения о проблемах, которые могут возникнуть при установке и запуске серверного по Windows 2016 Server Essentials. Этот раздел следует изучить перед установкой и запуском Windows Server 2016 Essentials в сети.

## <a name="client-computers"></a>Клиентские компьютеры

### <a name="install-all-available-critical-and-security-updates-from-windows-update"></a>Установите все доступные критические обновления и обновления безопасности из Центра обновления Windows.

Перед подключением клиентского компьютера к серверу убедитесь, что вы открыли Центр обновления Windows на клиентском компьютере и установили все доступные критические обновления и исправления безопасности.

### <a name="client-computer-restore-may-not-succeed-after-migration-to-windows-10"></a>Восстановление клиентских компьютеров после миграции на Windows 10 может не выполняться
 После обновления клиентского компьютера с Windows 8.1 до Windows 10, восстановление клиентского компьютера может работать неправильно. Необходимо повторно подключить клиент к Windows Server 2016 Essentials.

## <a name="enabling-tls-12-for-windows-server-essentials"></a>Включение TLS 1,2 для Windows Server Essentials
Чтобы обеспечить соответствие новейшим стандартам соответствия требованиям для Федеральная программа аккредитации облачных служб (FedRAMP), корпорация Майкрософт планирует отключить TLS-версии 1,1 и 1,0 и включить TLS 1,2 в Windows Server Essentials. Это делается и для клиентских, и для серверных компьютеров.

Сведения о включении TLS 1,2 см. в статье [Включение tls 1,2 на клиентах](/mem/configmgr/core/plan-design/security/enable-tls-1-2-client).
