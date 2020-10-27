---
title: Что нового в Windows Server версий 2004 и 20H2
description: Новые возможности Windows Server версий 2004 и 20H2
ms.topic: article
author: Heidilohr
ms.author: helohr
ms.date: 05/27/2020
ms.localizationpriority: high
ms.openlocfilehash: f44dcc7a1c7fab2d99f0358794bd5b2aedb87b75
ms.sourcegitcommit: b82dfbfdc5df1327feb8be053a760739b01e3031
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2020
ms.locfileid: "92255871"
---
# <a name="whats-new-in-windows-server-version-2004-and-20h2"></a>Новые возможности Windows Server версии 2004 и 20H2

>Применяется к: Windows Server (Semi-Annual Channel)

Подробные сведения о новых возможностях Windows приведены в этой [статье](whats-new-in-windows-server.md). В этом разделе описаны некоторые новые функции, доступные в Windows Server версий 2004 и 20H2.

Windows Server версии 20H2 — это очередной выпуск Windows Server версии 2004 в рамках Semi-Annual Channel. Эта версия ориентирована на повышение надежности, производительности и другие общие улучшения, но не содержит новых функций. Как и в случае с другими выпусками Semi-Annual Channel, она поддерживается в течение 18 месяцев после выпуска. Дополнительные сведения о датах поддержки выпусков Semi-Annual Channel см. в разделе [Информация о выпуске Windows Server](windows-server-release-info.md).

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
