---
title: Перенос ролей и компонентов
description: Сведения о том, как перенести роли и компоненты в более новую версию Windows Server.
ms.date: 08/28/2019
ms.topic: article
ms.assetid: 0f78ef4c-dd12-4b1b-8c6e-251dd803c5d1
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 029f3c2b2857dba88af0e5c7b584e257c579d063
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87959582"
---
# <a name="migrating-roles-and-features-in-windows-server"></a>Миграция ролей и компонентов в Windows Server

> Применяется к: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Эта страница содержит ссылки на информацию и инструменты, которые помогут вам в процессе переноса ролей и компонентов в более новую версию Windows Server. Вы можете перенести файловые серверы и хранилище с помощью [службы миграции хранилища](../storage/storage-migration-service/overview.md), в то время как многие другие роли и компоненты можно перенести с помощью средств миграции Windows Server. Это набор командлетов PowerShell, которые были введены в Windows Server 2008 R2 для переноса ролей и компонентов.

Руководства по миграции охватывают перенос определенных ролей и компонентов с одного сервера на другой (не обновление на месте). Если в руководствах не указано иное, поддерживается перенос между физическими и виртуальными компьютерами, а также между серверами Windows Server, для которых была выполнена полная установка, и серверами, для которых была выполнена только установка основных серверных компонентов.

## <a name="before-you-begin"></a>Перед началом работы

Перед началом переноса ролей и компонентов убедитесь, что исходный и целевой серверы работают под управлением операционных систем с последними пакетами обновления, которые для них доступны.

> [!NOTE]
> При миграции или обновлении до любой версии Windows Server следует просмотреть и понять [политику сроков поддержки](https://support.microsoft.com/lifecycle) и период времени для этой версии и плана соответственно. Вы можете [найти информацию о сроках](https://support.microsoft.com/lifecycle) для определенного выпуска Windows Server, который вас интересуют.

## <a name="windows-server-2019"></a>Windows Server 2019

Для переноса файловых серверов и хранилища на Windows Server 2019 или Windows Server 2016 рекомендуется использовать [службу миграции хранилища](../storage/storage-migration-service/overview.md). Сведения о переносе других ролей приведены в руководстве по Windows Server 2016 и Windows Server 2012 R2.

## <a name="windows-server-2016"></a>Windows Server 2016

Ниже приведены руководства по миграции для Windows Server 2016. Обратите внимание на то, что во многих случаях можно также использовать руководства по миграции для Windows Server 2012 R2.

- [Службы удаленных рабочих столов](../remote/remote-desktop-services/migrate-rds-role-services.md)
- [Веб-сервер (IIS)](https://www.iis.net/downloads/microsoft/web-deploy)
- [Службы Windows Server Update Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852339(v=ws.11))
- [Службы MultiPoint](../remote/multipoint-services/multipoint-services-migrate.md)

Для переноса файловых серверов в Windows Server 2019 или Windows Server 2016 рекомендуется использовать [службу миграции хранилища](../storage/storage-migration-service/overview.md).

## <a name="windows-server-2012-r2"></a>Windows Server 2012 R2

Следуйте инструкциям в этих руководствах для переноса ролей и компонентов с серверов под управлением Windows Server 2003, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 или Windows Server 2012 R2 на Windows Server 2012 R2. Средства миграции Windows Server в Windows Server 2012 R2 поддерживают перенос между различными подсетями.

- [Установка, использование и удаление средств миграции Windows Server](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134202(v=ws.11))
- [Руководство по переносу служб сертификатов Active Directory для Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486797(v=ws.11))
- [Перенос службы роли служб федерации Active Directory в Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486815(v=ws.11))
- [Руководство по обновлению и переносу служб управления правами Active Directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754277(v=ws.10))
- [Перенос файловых служб и служб хранилища в Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn479292(v=ws.11))
- [Перенос Hyper-V в Windows Server 2012 R2 с Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486799(v=ws.11))
- [Перенос сервера политики сети в Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831652(v=ws.11))
- [Перенос служб удаленных рабочих столов в Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn479239(v=ws.11))
- [Перенос служб обновления Windows Server Update Services в Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852339(v=ws.11))
- [Перенос кластерных ролей в Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn530779(v=ws.11))
- [Перенос DHCP-сервера в Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn495425(v=ws.11))

Теперь доступна электронная книга руководства по миграции Windows Server 2012 R2 и Windows Server 2012. Чтобы получить дополнительные сведения и скачать электронную книгу, ознакомьтесь с [коллекцией электронных книг по технологиям Майкрософт](https://download.microsoft.com/download/8/D/3/8D33661A-7E21-4FEE-9AAA-C17C3004B5AA/Windows-Migration-and-Upgrade-Guide.pdf).

## <a name="windows-server-2012"></a>Windows Server 2012

Следуйте инструкциям в этих руководствах для переноса ролей и компонентов с серверов под управлением Windows Server 2003, Windows Server 2008, Windows Server 2008 R2 или Windows Server 2012 на Windows Server 2012. Средства миграции Windows Server в Windows Server 2012 поддерживают перенос между различными подсетями.

- [Установка, использование и удаление средств миграции Windows Server](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134202(v=ws.11))
- [Перенос служб ролей для служб федерации Active Directory в Windows Server 2012](../identity/ad-fs/deployment/migrate-ad-fs-role-services-to-windows-server-2012.md)
- [Перенос центра регистрации работоспособности в Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831513(v=ws.11))
- [Перенос Hyper-V на Windows Server 2012 с Windows Server 2008 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574113(v=ws.11))
- [Перенос IP-конфигурации в Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574133(v=ws.11))
- [Перенос сервера политики сети в Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831652(v=ws.11))
- [Перенос служб печати и документов в Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134150(v=ws.11))
- [Перенос удаленного доступа в Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831423(v=ws.11))
- [Перенос служб обновления Windows Server Update Services в Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852339(v=ws.11))
- [Обновление контроллеров домена Active Directory до Windows Server 2012](../identity/ad-ds/deploy/upgrade-domain-controllers-to-windows-server-2012-r2-and-windows-server-2012.md)
- [Перенос кластеризованных служб и приложений в Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486790(v=ws.11))


Для получения дополнительных материалов по миграции ознакомьтесь с разделом [Перенос ролей и компонентов на Windows Server](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134039(v=ws.11)).

## <a name="windows-server-2008-r2"></a>Windows Server 2008 R2

Следуйте инструкциям в этих руководствах для переноса ролей и компонентов с серверов под управлением Windows Server 2003, Windows Server 2008 или Windows Server 2008 R2 на Windows Server 2008 R2. Средства миграции Windows Server в Windows Server 2008 R2 не поддерживают перенос между различными подсетями.

- [Установка средств миграции Windows Server, доступ к ним и удаление](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379545(v=ws.10))
- [Руководство по переносу служб сертификатов Active Directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee126170(v=ws.10))
- [Руководство по переносу служб домена Active Directory и DNS-сервера](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379558(v=ws.10))
- [Руководство по переносу BranchCache](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd548365(v=ws.10))
- [Руководство по переносу DHCP-сервера](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379535(v=ws.10))
- [Руководство по переносу файловых служб](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379487(v=ws.10))
- [Руководство по переносу HRA](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee791829(v=ws.10))
- [Руководство по переносу Hyper-V](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee849855(v=ws.10))
- [Руководство по переносу IP-конфигурации](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379537(v=ws.10))
- [Руководство по переносу группы и локальных пользователей](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379531(v=ws.10))
- [Руководство по переносу NPS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee791849(v=ws.10))
- [Руководство по переносу служб печати](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379488(v=ws.10))
- [Руководство по переносу служб удаленных рабочих столов](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff849223(v=ws.10))
- [Руководство по переносу RRAS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee822825(v=ws.10))
- [Общие сведения и задачи миграции Windows Server](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff400258(v=ws.10))
- [Руководство по переносу служб Windows Server Update 3.0 с пакетом обновления 2 (SP2)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee822826(v=ws.10))

Для получения дополнительных материалов по миграции ознакомьтесь с разделом [Migrate Server Roles to Windows Server 2008 R2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd365353(v=ws.10)) (Перенос ролей и компонентов в Windows Server 2008 R2).
