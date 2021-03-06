---
title: Что нового в Windows Server 2016 Essentials
description: Сведения о новых возможностях Windows Server 2016 Essentials.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: affff774-5fa6-4944-887a-9bfde05f6a3f
author: nnamuhcs
ms.author: geschuma
ms.openlocfilehash: ecce1760c4768d37936343604d9344a6d489c8cc
ms.sourcegitcommit: efc49ff9062f943abe36c5b6206096315723f56d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "90571333"
---
# <a name="whats-new-in-windows-server-2016-essentials"></a>Что нового в Windows Server 2016 Essentials

> Область применения: Windows Server 2016 Essentials

Ниже приведены новые и улучшенные функции Windows Server 2016 Essentials.

## <a name="integration-with-azure-site-recovery-services"></a>[Интеграция со службами Azure Site Recovery Services](azure-site-recovery-services-integration.md)

**Что он делает**  -- &reg; При сбое виртуальной машины, которая защищена, или при сбое на сервере узла, на котором выполняется Защищенная виртуальная машина, отработка отказа с Azure Site Recovery Services обеспечивает непрерывность бизнес-процессов до тех пор, пока локальная виртуальная машина или сервер узла не будут восстановлены и доступны.

**Как это работает** , Azure Site Recovery служб, предлагаемых в Microsoft Azure, обеспечивает репликацию виртуальных машин (ВМ) в режиме реального времени в хранилище службы архивации в Azure. Если сервер или сайт выйдет из строя из-за оборудования или другого сбоя, можно выполнить отработку отказа с помощью служб Azure Site Recovery Services, чтобы образ виртуальной машины, хранящийся в хранилище резервных копий, был подготовлен как работающая виртуальная машина в Azure. В сочетании с виртуальной сетью Azure клиентские компьютеры, ранее подключенные к локальному серверу, будут прозрачно подключаться к серверу, работающему в Azure.

## <a name="integration-with-azure-virtual-network"></a>[Интеграция с виртуальной сетью Azure](azure-virtual-network-integration.md)

**Что это делает**, так как организации делают свою работу в облачных вычислениях, они редко перемещают все ресурсы за один раз. Вместо этого они перемещают некоторые ресурсы в облако и сохраняют некоторые локальные. Таким образом, можно легко переместить организацию в облако с течением времени. Интеграция виртуальной сети Azure обеспечивает сетевую инфраструктуру, которая делает процесс прозрачным и управляемым.

Принцип **работы** . виртуальные сети Azure — это служба, предлагаемая в Microsoft Azure, которая позволяет организациям создавать виртуальную частную сеть типа "точка-точка" (P2P) или "сеть — сеть" (S2S), которая делает ресурсы, которые выполняются в Azure (например, виртуальные машины и хранилище), как если бы они находящегося в локальной сети для эффективного доступа к приложениям и ресурсам.

## <a name="support-for-larger-deployments"></a>[Поддержка более крупных развертываний](support-for-larger-deployments.md)

Некоторым крупным компаниям малого бизнеса требуется больше функций и возможностей для эффективной реализации Windows Server Essentials. Windows Server 2016 Essentials обеспечивает повышенную управляемость доменов, пользователей и устройств, добавляя поддержку более крупных развертываний с помощью следующих компонентов:

- несколько доменов
- несколько контроллеров домена
- возможность указать назначенный контроллер домена

См. также

- [Начало работы с Windows Server Essentials](get-started.md)
