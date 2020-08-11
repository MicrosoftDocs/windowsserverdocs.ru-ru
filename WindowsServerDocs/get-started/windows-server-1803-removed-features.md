---
title: Windows Server, версия 1803 — функции, которые были удалены
description: Сведения о компонентах, которые будут удалены или не будут поддерживаться в Windows Server версии 1803 и будущих версиях
ms.mktglfcycl: plan
ms.localizationpriority: medium
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.date: 10/22/2019
ms.openlocfilehash: 1d5a439a08cba15bd7ed37be8bb25f415cd16b46
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993620"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1803"></a>Удаленные или подлежащие замене компоненты в Windows Server версии 1803

> Применяется к: Windows Server версии 1803

В каждом выпуске Windows Server добавляются новые компоненты и возможности. Иногда мы также удаляем компоненты и функциональные возможности. Как правило, это происходит, когда мы добавляем улучшенную функцию. Ниже приведены подробные сведения о функциях и возможностях, которые были удалены в Windows Server версии 1803.

> [!TIP]
> - Ранний доступ к сборкам Windows Server можно получить, вступив в [Программу предварительной оценки Windows](https://insider.windows.com), — это отличный способ для проверки изменений в функциональных возможностях.
> - У вас есть вопросы о других выпусках? См. сведения об [удаленных или подлежащих замене компонентах в Windows Server](../get-started-19/removed-features.md).

**Этот список не является исчерпывающим и может быть изменен**.

## <a name="features-we-removed-in-this-release"></a>Компоненты, которые мы удалили в этом выпуске

Мы удалили следующие компоненты и функциональные возможности из установленного образа продукта в Windows Server версии 1803. Приложения или код, которые зависят от этих компонентов, не будут работать в этом выпуске, если вы не используете какой-либо альтернативный метод.

| Функция    | Вместо этого можно использовать... |
| ----------- | -------------------- |
| [Служба репликации файлов](https://support.microsoft.com/help/4025991/windows-server-version-1709-no-longer-supports-frs)|Службы репликации файлов, представленные в Windows Server 2003 R2, замещаются функцией репликации DFS. Вам потребуется [перевести все контроллеры доменов, использующие FRS, на репликацию DFS с помощью SYSVOL](https://techcommunity.microsoft.com/t5/storage-at-microsoft/streamlined-migration-of-frs-to-dfsr-sysvol/ba-p/425405). |
| Виртуализация сети Hyper-V (HNV)|[Виртуализация сети](../networking/sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md) теперь включена в Windows Server как часть решения [Программно-определяемая сеть](../networking/sdn/software-defined-networking.md) (SDN), которое также включает в себя контроллер сети, балансировку нагрузки программного обеспечения, определяемую пользователем маршрутизацию и списки управления доступом. |

## <a name="features-were-no-longer-developing"></a>Компоненты, которые мы больше не разрабатываем

Мы прекращаем активную разработку этих компонентов и, возможно, удалим их из будущих обновлений. Некоторые компоненты заменены на другие компоненты или функции, в то время как другие компоненты теперь доступны в иных источниках.

>[!NOTE]
> Обратите внимание, что некоторые компоненты и роли, приведенные ниже, не включены в вариант установки Server Core, доступный в Windows Server версии 1803. Они *представлены* в варианте установки Server с возможностями рабочего стола, который мы последний раз выпустили для Windows Server 2016 и снова выпустим для Windows Server 2019.

Если вы хотите оставить отзыв о предстоящей замене какого-либо из этих компонентов, воспользуйтесь приложением [Центр отзывов](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app).

| Компонент или роль    | Вместо этого можно использовать... |
| ----------- | --------------------- |
| Бизнес-сканирование, также известное как распределенное управление сканированием (DSM)|[Функция управления сканированием](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd759124\(v%3dws.11\)) была введена в Windows Server 2008 R2 и обеспечивала безопасное сканирование и управление сканированием в организации. Мы больше не будем вкладывать усилия в этот компонент, и сейчас не существует устройств, которые бы его поддерживали. |
| Технологии туннелирования IPv4/6 (6to4, ISATAP и прямое туннелирование)|Функция 6to4 отключена по умолчанию начиная с Windows 10 версии 1607 (юбилейное обновление), ISATAP отключена по умолчанию начиная с Windows 10 версии 1703 (Creators Update), а прямое туннелирование всегда было отключено по умолчанию. Вместо этого используйте встроенную поддержку IPv6. |
| [Службы MultiPoint](../remote/multipoint-services/multipoint-services.md)|Мы больше не разрабатываем роль служб MultiPoint в составе Windows Server. Службы соединителя MultiPoint доступны в функции [Компонент по требованию](/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities) для Windows Server и Windows 10. Можно использовать [Службы удаленных рабочих столов](../remote/remote-desktop-services/welcome-to-rds.md), в частности, Узел сеансов служб удаленных рабочих столов для обеспечения связи RDP. |
| [Автономные пакеты символов](/windows-hardware/drivers/debugger/debugger-download-symbols) (MSI-файлы символов для отладки)|Мы больше не предлагаем пакеты символов в виде загружаемых MSI-файлов. Вместо этого [сервер символов (Майкрософт) станет хранилищем символов на основе Azure](/archive/blogs/windbg/update-on-microsofts-symbol-server). Если вам требуются символы Windows, подключитесь к серверу символов (Майкрософт), чтобы закэшировать символы в локальном режиме, или используйте файл манифеста с SymChk.exe на компьютере с доступом в Интернет. |
| [Брокер подключений к удаленному рабочему столу и узел виртуализации удаленных рабочих столов](../remote/remote-desktop-services/desktop-hosting-service.md) в установке основных серверных компонентов|В большинстве развертываний служб удаленных рабочих столов эти роли совместно размещаются с узлом сеансов удаленных рабочих столов (RDSH), что требует наличия Server с возможностями рабочего стола. Для обеспечения единообразия в RDSH мы изменяем эти роли, и они также будут требовать Server с возможностями рабочего стола. Мы больше не разрабатываем эти роли RDS для использования в [установке Server Core](../administration/server-core/what-is-server-core.md). Если вам необходимо [развернуть эти роли как часть инфраструктуры удаленного рабочего стола](../remote/remote-desktop-services/rds-deploy-infrastructure.md), можно [установить их в Windows Server 2016 с возможностями рабочего стола](getting-started-with-server-with-desktop-experience.md). <br/><br/>Эти роли также включаются в вариант установки с возможностями рабочего стола в Windows Server 2019. Их можно проверить в [сборке программы предварительной оценки Windows для Windows Server 2019](/windows-insider/at-work/), просто не забудьте выбрать образ LTSC. |
| [3D-видеоадаптер RemoteFX (vGPU)](../virtualization/hyper-v/deploy/deploy-graphics-devices-using-remotefx-vgpu.md)|Мы разрабатываем новые параметры ускорения графики для виртуализованных сред. В качестве альтернативы также можно использовать [Дискретное назначение устройств (DDA)](../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md). |
| [Политика программных ограничений](../identity/software-restriction-policies/software-restriction-policies.md) в групповой политике|Вместо использования политики программных ограничений в групповой политике можно использовать [AppLocker](/windows/security/threat-protection/applocker/applocker-overview) или [управление приложениями в Защитнике Windows](/windows/security/threat-protection/windows-defender-application-control) для управления тем, к каким приложениям пользователи могут получить доступ и какой код может выполняться в ядре. |
| Дисковые пространства в общей конфигурации с использованием структуры SAS|Вместо этого разворачивайте [локальные дисковые пространства](../storage/storage-spaces/storage-spaces-direct-overview.md). Локальные дисковые пространства поддерживают использование сертифицированных HLK корпусов SAS, но в конфигурации без общего доступа, как описано в [требованиях к оборудованию локальных дисковых пространств](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md). |
| Режим Windows Server Essentials|Мы больше не разрабатываем роль режима Essentials для Windows Server Standard и SKU Windows Server Datacenter. Если вам требуется простое серверное решение для предприятий малого и среднего бизнеса, проверьте наше новое решение [Microsoft 365 для бизнеса](https://www.microsoft.com/microsoft-365/business) или используйте [Windows Server 2016 Essentials](/windows-server-essentials/get-started/get-started). |