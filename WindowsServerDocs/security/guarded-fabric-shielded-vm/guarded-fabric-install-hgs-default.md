---
title: Установка HGS в новом лесу
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: c18c14435c93d08c98b1a765fd820294a273a575
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939548"
---
# <a name="install-hgs-in-a-new-forest"></a>Установка HGS в новом лесу

>Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016

## <a name="add-the-hgs-server-role"></a>Добавление роли сервера HGS

Выполните следующие команды в сеансе PowerShell с повышенными привилегиями, чтобы добавить роль сервера HGS и установить HGS.

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)]

## <a name="install-hgs"></a>Установка HGS

[!INCLUDE [Install HGS by default](../../../includes/install-hgs-default.md)]

## <a name="next-steps"></a>Дальнейшие действия

- Дальнейшие действия по настройке аттестации на основе TPM см. в статье [Инициализация кластера HGS с помощью режима TPM в новом выделенном лесу (по умолчанию)](guarded-fabric-initialize-hgs-tpm-mode-default.md).
- Дальнейшие действия по настройке аттестации ключа узла см. в статье [Инициализация кластера HGS с помощью режима ключей в новом выделенном лесу (по умолчанию)](guarded-fabric-initialize-hgs-key-mode-default.md).
- Дальнейшие действия по настройке аттестации на основе администратора (не рекомендуется в Windows Server 2019) см. в статье [Инициализация кластера HGS с помощью режима AD в новом выделенном лесу (по умолчанию)](guarded-fabric-initialize-hgs-ad-mode-default.md).

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Инициализация HGS](guarded-fabric-initialize-hgs.md)


