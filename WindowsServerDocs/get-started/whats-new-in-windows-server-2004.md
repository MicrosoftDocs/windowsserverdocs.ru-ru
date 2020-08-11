---
title: Новые возможности Windows Server версии 2004
description: Новые возможности Windows Server, версия 2004
ms.topic: article
author: Heidilohr
ms.author: helohr
ms.date: 05/27/2020
ms.localizationpriority: high
ms.openlocfilehash: 210aa06711c67af46d35a38fe4308bc4060691e8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957011"
---
# <a name="whats-new-in-windows-server-version-2004"></a>Новые возможности Windows Server версии 2004

>Применяется к: Windows Server (Semi-Annual Channel)

Подробные сведения о новых возможностях Windows приведены в этой [статье](whats-new-in-windows-server.md). В этом разделе описаны некоторые новые функции, доступные в Windows Server версии 2004.

## <a name="server-core-container-improvements"></a>Улучшения контейнеров Server Core

Мы уменьшили общий размер образов контейнеров Server Core, чтобы повысить скорость скачивания и производительность. Добавлены следующие улучшения:

- Чтобы уменьшить размер образа, мы удалили большинство образов NGEN из образа контейнера Server Core.
- Образы среды выполнения .NET Framework, созданные на основе образов контейнеров Server Core, теперь оптимизированы для приложений ASP.NET и для выполнения скриптов Windows PowerShell.
- Разработчики .NET обеспечили наличие только одной копии каждого образа NGEN, чтобы уменьшить размер образов .NET Framework.

Для предоставления более наглядной информации о размерах этих контейнеров в следующей таблице приводится сравнение текущей версии контейнера [в обновлении системы безопасности за май 2020 г.](https://support.microsoft.com/help/4561769/windows-server-containers-for-may-2020) (также известного как обновление 5B) с предыдущими версиями.

| Версия контейнера | Размер файла для скачивания | Размер на диске |
|---|---|---|
| Windows Server версии 1903 | 2,311 ГБ | 5,1 ГБ |
| Windows Server, версия 1909 | 2,257 ГБ | 4,97 ГБ |
| Windows Server версии 2004 | 1,830 ГБ | 3,98 ГБ |

Дополнительные сведения об обновлении Windows Server версии 2004 см. в [нашей записи блога](https://techcommunity.microsoft.com/t5/containers/windows-server-version-2004-now-available/ba-p/1419194). Больше общих сведений можно в статье [Обновление контейнеров Windows Server](/virtualization/windowscontainers/deploy-containers/update-containers/).
