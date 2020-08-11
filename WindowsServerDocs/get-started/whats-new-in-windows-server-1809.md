---
title: Новые возможности Windows Server версии 1809
description: Новые возможности в Windows Server версии 1809
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 05/21/2019
ms.localizationpriority: high
ms.openlocfilehash: cb3bf10b0c89f60a5cebb7109ebc4a7de46f8961
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941643"
---
# <a name="whats-new-in-windows-server-version-1809"></a>Новые возможности Windows Server версии 1809

>Область применения. Windows Server (Semi-Annual Channel)

Подробные сведения о новых возможностях Windows приведены в этой [статье](whats-new-in-windows-server.md). В этом разделе описаны некоторые новые функции в Windows Server версии 1809.

## <a name="container-networking-with-kubernetes"></a>Работа с сетевыми подключениями контейнеров с помощью Kubernetes

[Средства работы с сетевыми подключениями контейнеров с использованием Kubernetes](../networking/sdn/technologies/containers/container-networking-overview.md) в Windows Server 2019 значительно повышают удобство использования Kubernetes в Windows за счет улучшения устойчивости сети платформы и поддержки подключаемых модулей сетевых подключениях контейнеров.
Кроме того, встроенные инструменты позволяют обеспечить сетевую безопасность служб Linux и Windows в рабочих нагрузках, развертываемых на платформе Kubernetes.

## <a name="group-managed-service-accounts-for-containers"></a>Групповые управляемые учетные записи служб для контейнеров

В Windows Server версии 1809 улучшена масштабируемость и надежность контейнеров, которые используют групповые управляемые учетные записи служб (gMSA) для доступа к сетевым ресурсам.

## <a name="host-device-access-for-containers"></a>Доступ к главному устройству для контейнеров

Вы можете назначать простые шины контейнерам Windows Server с изолированными процессами.
Приложения, работающие в контейнерах, которым необходимо взаимодействовать по SPI, I2C, GPIO и UART/COM, теперь могут делать это.

## <a name="additional-features"></a>Дополнительные возможности
В дополнение к функциям, которые появились в Windows Server версии 1809, следующие новые функции и возможности для [Windows Server 2019](../get-started-19/get-started-19.md) также применимы к Windows Server версии 1809:

* Улучшения контейнеров
* HTTP/2
* Поддержка Kubernetes
* Контейнеры Linux в Windows
* [Передача данных с помощью алгоритма Low Extra Delay Background Transport (LEDBAT)](https://techcommunity.microsoft.com/t5/networking-blog/bg-p/NetworkingBlog)
* Повышение производительности сети для виртуальных рабочих нагрузок
* [Функция совместимости приложений основных серверных компонентов по запросу (FOD)](../get-started-19/install-fod-19.md)
* [Служба миграции хранилища (SMS)](../storage/whats-new-in-storage.md#storage-spaces-direct)
* Реплика хранилища
* Системная аналитика
* Advanced Threat Protection в Защитнике Windows (ATP)
* Exploit Guard для ATP в Защитнике Windows
* [Служба времени Windows](../networking/windows-time-service/insider-preview.md)
