---
title: Синхронизация файлового сервера с облаком с помощью Синхронизации файлов Azure
description: Используйте Синхронизация файлов Azure для централизации файловых ресурсов Организации в Azure, обеспечивая гибкость, производительность и совместимость локального файлового сервера. Синхронизация файлов Azure преобразует Windows Server в быстрый кэш файлового ресурса Azure с помощью дополнительного компонента распределения по уровням облака.
ms.topic: article
author: fauhse
ms.author: fauhse
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 56937ad0351a1421ab64b93351d7fa5f6d9f4fe8
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766687"
---
# <a name="sync-your-file-server-with-the-cloud-by-using-azure-file-sync"></a>Синхронизация файлового сервера с облаком с помощью Синхронизации файлов Azure

>Применяется к: Windows Admin Center, ознакомительная версия Windows Admin Center

Используйте Синхронизация файлов Azure для централизации файловых ресурсов Организации в Azure, обеспечивая гибкость, производительность и совместимость локального файлового сервера. Синхронизация файлов Azure преобразует Windows Server в быстрый кэш файлового ресурса Azure с помощью дополнительного компонента распределения по уровням облака. Для локального доступа к данным вы можете использовать любой протокол, доступный в Windows Server, в том числе SMB, NFS и FTPS.

После синхронизации файлов в облаке можно подключить несколько серверов к одной общей папке Azure для синхронизации и кэширования содержимого локально — разрешения (ACL) всегда передаются в транспорт. Служба файлов Azure предоставляет возможность создания моментальных снимков, которые могут создавать разностные моментальные снимки файлового ресурса Azure. Эти моментальные снимки можно даже подключить как сетевые диски только для чтения через SMB для простоты просмотра и восстановления. В сочетании с распределением по уровням облака выполнение локального файлового сервера никогда не было проще.

Дополнительные сведения см. в разделе [Планирование развертывания Синхронизация файлов Azure](/azure/storage/files/storage-sync-files-planning).