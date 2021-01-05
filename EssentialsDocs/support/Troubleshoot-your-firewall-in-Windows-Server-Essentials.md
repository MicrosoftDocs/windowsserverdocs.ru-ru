---
title: Устранение неполадок брандмауэра в Windows Server Essentials
description: Узнайте, как использовать мастер восстановления повсеместного доступа при возникновении проблем с удаленным доступом.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 51d94b67-8b9b-4159-80dd-f652d73a43cb
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 3cf84844a0bbca8128df1429c843d3e565318f95
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810071"
---
# <a name="troubleshoot-your-firewall-in-windows-server-essentials"></a>Устранение неполадок брандмауэра в Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 При возникновении проблем с удаленным доступом запустите мастер исправления повсеместного доступа.

### <a name="to-run-the-repair-anywhere-access-wizard"></a>Запуск мастера исправления повсеместного доступа

1. Откройте панель мониторинга.

2. Нажмите кнопку **Параметры**, затем откройте вкладку **Повсеместный доступ** и щелкните **Исправить**.

3. Следуйте инструкциям мастера исправления повсеместного доступа.

   Если вы применяете расширенную настройку сети или используете брандмауэр другого разработчика, может потребоваться открыть дополнительные порты брандмауэра. Описанные в следующей таблице порты зарегистрированы в Internet Assigned Numbers Authority (IANA).

|Номер порта|Описание|
|-----------------|-----------------|
|65500|Веб-служба сертификатов|
|65510 и 65515|Веб-сайт развертывания клиентских компьютеров|
|65520|Веб-служба для клиентских компьютеров Mac|
|65532|Платформа поставщика для связи с сервером замыканием на себя|
|6602|Платформа поставщика для обмена данными между сервером и клиентскими компьютерами|

## <a name="see-also"></a>См. также раздел

-   [Раздел об использовании удаленного веб-доступа](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [Управление удаленным веб-доступом](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [Управление повсеместным доступом](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Управление Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)

-   [Поддержка Windows Server Essentials](../support/Support-Windows-Server-Essentials.md)

