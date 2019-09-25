---
title: Общие сведения об обновлениях Windows Server | Документация Майкрософт
description: Ознакомьтесь с некоторыми общими сведениями об обновлении Windows Server, а также о том, что следует учесть перед выполнением фактического обновления.
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/10/2019
ms.openlocfilehash: 6f57e52657ca3c80c92d56c54ea87e43aabd1e99
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/19/2019
ms.locfileid: "71124794"
---
# <a name="overview-about-windows-server-upgrades"></a>Общие сведения об обновлениях Windows Server

Процесс обновления до более новой версии Windows Server может сильно различаться в зависимости от того, с какой операционной системой вы начинаете работу, и от выполняемых вами путей. Мы используем следующие термины для различения различных действий, которые могут быть задействованы в новом развертывании Windows Server.

- **Обновления.** Также называется «обновление на месте». Вы переходите с более старой версии операционной системы на более новую, сохраняя на том же физическом оборудовании. **Это метод, который мы будем рассматривать в этом разделе.**

    >[!Important]
    >Обновления на месте могут также поддерживаться компаниями общедоступных или частных облаков; Однако для получения подробных сведений необходимо уточнить у поставщика облачных служб. Кроме того, вы не сможете выполнить обновление на месте на любом сервере Windows, настроенном для **загрузки с виртуального жесткого диска**.

- **Систему.** Также называется "чистой установкой". Вы переходите от более старой версии операционной системы к более новой версии, удаляя старую операционную систему.

- **Преобразования.** Переход с более ранней версии операционной системы на более новую версию операционной системы осуществляется путем передачи в другой набор оборудования или виртуальной машины.

- **Последовательное обновление ОС кластера.** Обновление операционной системы узлов кластера выполняется без остановки Hyper-V или масштабируемый файловый сервер рабочих нагрузок. Эта функция позволяет избежать простоя, который может нарушать соглашения об уровне обслуживания. Дополнительные сведения см. в статье [последовательное обновление операционной системы кластера](../failover-clustering/cluster-operating-system-rolling-upgrade.md) .

- **Преобразование лицензий.** Преобразуйте определенный выпуск выпуска в другой выпуск того же выпуска за один шаг, используя простую команду и соответствующий лицензионный ключ. Мы вызываем это «преобразование лицензий». Например, если ваш сервер работает под управлением Windows Server2016 Standard, вы можете преобразовать его в Windows Server2016 Datacenter.

## <a name="which-version-of-windows-server-should-i-upgrade-to"></a>Какую версию Windows Server следует обновить до?

Рекомендуется выполнить обновление до последней версии Windows Server: Windows Server 2019. Использование последней версии Windows Server позволяет использовать новейшие функции, включая новейшие функции безопасности, и обеспечивает лучшую производительность.

Однако мы понимаем, что это не всегда возможно. Приведенную ниже схему можно использовать для определения версии Windows Server, до которой можно выполнить обновление, в зависимости от версии, на которой Вы находитесь.

![Доступные пути обновления на месте](media/upgrade-paths.png)

Windows Server обычно может обновляться по крайней мере один, а иногда даже две версии. Например, Windows Server 2012 R2 и Windows Server 2016 могут быть обновлены на месте до Windows Server 2019.

Вы также можете обновить ознакомительную версию операционной системы до розничной версии, от старой розничной версии до более новой версии или, в некоторых случаях, из выпуска операционной системы с корпоративной лицензией к обычному розничному выпуску. Дополнительные сведения о параметрах обновления, отличных от обновления на месте, см. в разделе [варианты обновления и преобразования для Windows Server](../get-started/supported-upgrade-paths.md).