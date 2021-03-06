---
description: 'Дополнительные сведения: Microsoft Hyper-V Server 2016'
title: Microsoft Hyper-V Server 2016
ms.topic: how-to
ms.assetid: f815ada0-4c63-4e73-9c24-dc5eb21526c7
ms.author: benarm
author: BenjaminArmstrong
ms.date: 07/26/2017
ms.openlocfilehash: a894b4d8bf9055c96f4d391521f1bdf798090e64
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948140"
---
# <a name="microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016

Microsoft Hyper-V Server 2016 — это автономный \- продукт, который содержит только гипервизор Windows, модель драйвера Windows Server и компоненты виртуализации. Она предоставляет простое и надежное решение для виртуализации, помогающее повысить эффективность использования сервера и снизить затраты.

Технология гипервизора Windows в Microsoft Hyper-V Server 2016 аналогична \- роли Hyper V в Windows server 2016. Таким образом, большая часть содержимого, доступного для \- роли Hyper V в Windows Server 2016, также применима к Microsoft Hyper-V Server 2016.

## <a name="hyper-v-server-resources-for-it-pros"></a>\-Ресурсы по Hyper-V Server для ИТ-специалистов

|Задания|Ресурсы|
|-|-|
|![Соответствует символу требований](media/All_Symbols_MeetsRequirements.png)|**Оцените Hyper-V**<p>-   [Обзор технологии Hyper-V](hyper-v-technology-overview.md)<br />- [Новые возможности Hyper-V в Windows Server 2016](what-s-new-in-hyper-v-on-windows.md)<br />-   [Требования к системе для Hyper-V в Windows Server 2016](system-requirements-for-hyper-v-on-windows.md)<br />-   [Поддерживаемые гостевые операционные системы Windows для Hyper-V](supported-windows-guest-operating-systems-for-hyper-v-on-windows.md)<br />-   [Поддерживаемые виртуальные машины Linux и FreeBSD](supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)<br />-   [Совместимость функций по поколениям и гостям](hyper-v-feature-compatibility-by-generation-and-guest.md)<p>**Планирование Hyper-V**<p>— Решите, какое [поколение виртуальных машин](plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md)  соответствует вашим потребностям. <br/>— Если вы перемещаете или импортируете виртуальные машины, решите, когда следует [обновлять версию](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md). <br />- [Масштабируемости](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [Сети](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [Бюллетеня](plan/plan-hyper-v-security-in-windows-server.md)|
|![Получить символ начала работы](media/All_Symbols_GetStarted.png)|**Приступая к работе с Hyper-V Server**<p>[Загрузка и установка Microsoft Hyper \- V Server 2016](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016). При этом устанавливается низкоуровневая оболочка Windows, модель драйвера Windows Server и компоненты виртуализации. Это похоже на выполнение варианта установки Server Core в Windows Server 2016 и \- роли Hyper V.|
|![Управление символом](media/All_Symbols_Administrator.png)|**Настройка сервера Hyper-V и управление им**<p>\-Сервер Hyper-V не имеет графического графического пользовательского \( интерфейса \) . Для настройки и управления сервером Hyper V можно использовать следующие средства \- .<p>-   [Настройте установку основных серверных компонентов Windows server 2016 с помощью SCONFIG. cmd](../../get-started/sconfig-on-ws2016.md) , чтобы обновить параметры домена или рабочей группы, изменить параметры центр обновления Windows, включить удаленное управление и многое другое.<br />— Используйте обычную [командную строку](../../administration/windows-commands/windows-commands.md) для команд, недоступных в SCONFIG.<br />— Используйте [ \- Диспетчер Hyper-v](./manage/remotely-manage-hyper-v-hosts.md) или [Virtual Machine Manager](/system-center/vmm) для удаленного управления сервером Hyper- \- v. Чтобы использовать \- Диспетчер Hyper v, [установите роль Hyper \- v в Windows 10](/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) или [Windows Server 2016](get-started/install-the-hyper-v-role-on-windows-server.md).<br />— См. раздел [Установка Server Core](../../get-started/getting-started-with-server-core.md) для дополнительных вариантов управления основными функциями сервера, которые не относятся к Hyper \- V. Большинство описанных методов управления также работают с Hyper \- V Server.<p>**Настройка виртуальных машин Hyper V и управление ими \-**<p>-   [Создание виртуального коммутатора для виртуальных машин Hyper-V](get-started/create-a-virtual-switch-for-hyper-v-virtual-machines.md)<br />-   [Создание виртуальной машины в Hyper-V](get-started/create-a-virtual-machine-in-hyper-v.md)<br />-   [Выбор контрольных точек "Стандартный" или "Рабочая"](manage/choose-between-standard-or-production-checkpoints-in-hyper-v.md)<br />-   [Включение и отключение контрольных точек](manage/enable-or-disable-checkpoints-in-hyper-v.md)<br />-   [Управление виртуальными машинами Windows с помощью PowerShell Direct](manage/manage-windows-virtual-machines-with-powershell-direct.md) <p>**Развертывание**<p>-   [Настройка узлов для динамической миграции без отказоустойчивой кластеризации](deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)<br />- [Обновление узлов кластера Windows Server](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)<br />- [Обновление версии виртуальной машины](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)<br />|
