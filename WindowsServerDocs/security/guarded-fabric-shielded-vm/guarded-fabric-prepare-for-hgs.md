---
title: Проверка предварительных требований для HGS
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: a8a0f469e2fe0052a3894a2f8b59a4a3ab233a9e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971301"
---
# <a name="review-prerequisites-for-the-host-guardian-service"></a>Проверка предварительных требований для службы защиты узла

>Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016


В этом разделе рассматриваются предварительные требования для HGS и начальные шаги для подготовки к развертыванию HGS.

## <a name="prerequisites"></a>Предварительные требования

-   **Оборудование**: можно запустить HGS на физических компьютерах или виртуальных машинах, но рекомендуется использовать физические компьютеры.

    Если вы хотите запустить HGS как физический кластер из трех узлов (для обеспечения доступности), необходимо иметь три физических сервера. (Для кластеризации рекомендуется, чтобы на трех серверах было очень похожее оборудование.)

-   **Операционная система**: аттестация ключа узла требует выпуска Windows Server 2019 Standard или Datacenter Edition с [аттестацией v2](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#versioned-attestation-policies). Для аттестации на основе доверенного платформенного модуля HGS может работать под управлением Windows Server 2019 или Windows Server 2016, Standard или Datacenter Edition.

-   **Роли сервера**: служба защиты узла и вспомогательные роли сервера.

-   **Разрешения и привилегии конфигурации для домена структуры (узла)**. необходимо настроить перенаправление DNS между доменом (узлом) и доменом HGS.

## <a name="upgrading-hgs"></a>Обновление HGS

Если вы уже развернули HGS и хотите обновить свою операционную систему, следуйте инструкциям [по обновлению, чтобы обновить](guarded-fabric-upgrade-to-2019.md) серверы HGS и Hyper-V до последней ОС.

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Получение сертификатов для HGS](guarded-fabric-obtain-certs.md)